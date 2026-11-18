# Issue

**Title:** agent: an attachment-only chat turn is a question, not an empty one

## Description

.

## The bug

Attaching a file and pressing send without typing anything was answered with
`-3 Empty question.` before the agent was ever reached. `chat_handler` judged
emptiness on the message **text** alone, so a turn whose entire content *is* the
attachment could not be sent — the one gesture a person makes with a photo of a
lab report. Adding any text at all made the same request work.

## The change

Two seams, in `mirobody/agent/chat/`:

1. **`service.py`** — judge emptiness on the whole turn: reject only when there
   is neither text nor an attachment that names a `file_key`.
2. **`adapters/base.py`** — normalise the turn **once**, at the top of
   `handle_request`, before the `asyncio.gather`: a turn that carries files but
   no words gets a stand-in question in the request's own language, so it
   never carries a zero-length user message.

The second half is the part that matters, and it is why this is not a one-line
guard change. Relaxing the guard alone would send `HumanMessage(content="")`
down the pipeline, and that is not a harmless no-op:

* **It is provider-dependent, so it fails in production and not in testing.**
  Measured through OpenRouter, a system message plus one empty user message:

  | model | result |
  | --- | --- |
  | `anthropic/claude-sonnet-5` | **400** `messages: at least one message is required` |
  | `openai/gpt-5.4-mini` | 200, tolerated |
  | `deepseek/deepseek-v4-flash` | 200, tolerated |

  What Anthropic rejects is the **zero-length text block itself**, and one such
  block 400s the whole request. Note that on the DeepAgent path the turn is not
  literally message-less: `_attachment_reminder` appends a non-empty
  `HumanMessage` whenever `file_list` is non-empty, so the empty message travels
  *alongside* it and still fails the request.

* **A failed turn does not go away.** LangGraph checkpoints a turn's input
  **before** the model node runs, and the DeepAgent graph's `thread_id` is the
  `session_id`. Verified with a graph whose model node always raises — after the
  failure the thread still holds `SystemMessage('[uploads notice]')` and
  `HumanMessage('')`, to be replayed on every later turn of that session.

## Why `handle_request` and not message-build time

The first version of this PR substituted the stand-in in
`_prepare_agent_kwargs`, one layer too late. `params.question` is what the whole
turn keys on, and three things read it before the message is ever built:

* `_prepare_agent_kwargs` folds `current_turn_note` into `question` **first**, so
  once a resume hint existed the substitution never ran and the user message
  became a bare time hint asking nothing at all;
* the `question` kwarg stayed `""`, and `BaseAgent` renders its prompt with
  `detect_language(question)` — `detect_language("")` is English, so a Chinese
  user who attached a report and typed nothing got an English-instructed prompt;
* `_save_question_if_needed` tests `params.question`, so the turn wrote no row to
  `th_messages` — an assistant answer whose `question_id` points at a row that
  does not exist, a chat that reloads as an answer with no question, and a
  session title stuck at "New Session".

Setting `params.question` once, before the gather, makes persistence, the
summary/title, the note concatenation, the `question` kwarg and the message agree
by construction. `_prepare_agent_kwargs` needs no branch at all.

The stand-in lives in the repo's own i18n layer
(`mirobody/utils/locales/chat.json`, via `utils/i18n.t`), which covers
zh/en/fr/ja/es. `LANGUAGE_CODES` was missing `zh-tw`/`zh-hant`, which would have
sent Traditional Chinese to English; they now map to `zh`, since we ship a
`README.zh-TW.md`.

`has_attachment` (one definition, `chat/model.py`) is what both the guard and the
substitution test. Truthiness is a different question: `[{}]`, and even
`{"file_list": "x"}`, would otherwise pass the guard and then promise the model
an attachment while `/uploads/` is empty and `_attachment_reminder` returns
`None`.

## Verification

Against a running stack (`./deploy.sh`, OpenRouter key configured), the same
request before and after.

**Before** — refused at the door, the agent never runs:

![before](https://raw.githubusercontent.com/abietic/mirobody/evidence/attachment-only-turn/.evidence/before.png)

**After** — the turn reaches the agent, which reads the attached lab-report
image and answers with its values; a follow-up question in the **same session**
still resolves the image, so the thread is not poisoned:

![after](https://raw.githubusercontent.com/abietic/mirobody/evidence/attachment-only-turn/.evidence/after.png)

The three seams the review found, terminal output verbatim:

```
$ python check41.py
### the stand-in, per language
  zh        -> 请阅读我这次上传的文件，并给出解读。
  zh-TW     -> 请阅读我这次上传的文件，并给出解读。
  zh-Hant   -> 请阅读我这次上传的文件，并给出解读。
  en        -> Please read the file(s) I attached to this message and tell me what they say.
  fr        -> Merci de lire le ou les fichiers que j'ai joints à ce message et de m'expliquer ce qu'ils contiennent.
  ja        -> 今回アップロードしたファイルを読んで、内容を説明してください。
  es        -> Por favor, lee el archivo o los archivos que he adjuntado a este mensaje y explícame qué dicen.
  <empty>   -> Please read the file(s) I attached to this message and tell me what they say.

### the guard (chat_handler's test)
  has_attachment([]  ) -> False
  has_attachment([{}]) -> False
  has_attachment('x' ) -> False
  has_attachment(None) -> False
  has_attachment([{'file_key': 'web_uploads/k.png', 'file_name': 'labreport.png'}]) -> True

### the turn, normalised in handle_request, with a resume hint
  question kwarg : '请阅读我这次上传的文件，并给出解读。'
  user message   : '请阅读我这次上传的文件，并给出解读。\n\n(Context: about 3 hours have passed ...)'
```

`detect_language` on that stand-in returns `Simplified Chinese`, where the empty
string returned `English`.

Gates from CONTRIBUTING.md, run against this branch:

```
$ python -m pytest -q
197 passed, 1 warning in 9.51s

$ lint-imports
Contracts: 2 kept, 0 broken.
```

## Two notes for the reviewer

* The "after" capture is from one of several post-fix runs. A later run of the
  identical request hit #40 — an intermittent, unrelated race where `ls` lists
  an attachment that `read_file` then cannot open. That run still reached the
  agent and answered normally; it just could not read the file. The two runs
  differ only in whether that race fired, and #40 is filed separately.
* The screenshots are served from a throwaway `evidence/attachment-only-turn`
  branch on the fork, purely so they render here. Nothing in this PR depends on
  it and it can be deleted after review. They are typeset reconstructions rather
  than captures; the terminal blocks above are raw.

## Product decision left open

The turn now persists: `th_messages` gets a user row carrying the stand-in, and
the session takes a title from it. What remains a product call is the **wording**
of that sentence and whether the UI should render it as something other than
text the user typed — a distinct `message_type` is the lever if we want that.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `85647b8c4d16`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.