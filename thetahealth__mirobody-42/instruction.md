# Issue

**Title:** agent: name this turn's uploads by what the request called them

## Description

. Independent of #41 — different files, no conflict.

## The bug

`ls /uploads` listed an attachment that `read_file` then could not open, and
`glob` for that name found nothing — all inside one turn, seconds apart. The
agent told the user their successfully uploaded report was unreadable and asked
them to send it again.

## Root cause

The two ends addressed the file by different names.

* `_attachment_reminder` (`deep_agent.py`) tells the model to read
  `/uploads/<name>` using the name from the **request payload** — the client's
  filename.
* `ThFilesBackend._files` derived the mount's paths from **`th_files.file_name`**.

Those are not the same string. `handlers/base.py::_extract_abstract` asks an LLM
for a descriptive name during upload processing and **overwrites the column with
it** — `labreport3.png` becomes `2026-08-22_Lab_Report_Patient_Demo1.png`.

Extraction runs concurrently with the agent, so that write lands *during* the
turn, which is what made it look intermittent:

```
ls        -> before the rename -> ['/uploads/labreport3.png']   ok
          -- rename commits --
read_file -> after  the rename -> file_not_found
glob      -> after  the rename -> No files found
```

`glob` agreeing with `read_file` was the tell: by then the file really did have
another name. No query ever failed — the row came back every time, under a name
that had moved.

## The change

`/uploads/` names this turn's attachments by what the request attached them
under. The mount and the reminder now come from one source, so no rename can
move a path out from under the model mid-turn.

`/library/` is unchanged and still shows the stored, LLM-generated name: it is
discovered with `ls`, nothing announces it in advance, and there the descriptive
name is the useful one.

## Verification

![before and after](https://raw.githubusercontent.com/abietic/mirobody/evidence/attachment-only-turn/.evidence/fix40.png)

Deterministically, for a file whose rename had already landed — before, the
mount served `/2026-08-22_Lab_Report_Patient_Demo1.png` while the model was told
`/uploads/labreport3.png` and `_fetch_row` missed; after, both are
`/uploads/labreport3.png` and it hits. `/library/` still lists the descriptive
names.

End to end on a fresh upload, with the rename committing **827 ms before** the
read — the exact timing that used to fail:

```
01:56:16,793  Updating th_files with 1 processed files       <- rename lands
01:56:17,620  [Tool Call] read_file '/uploads/labreport4.png'
              -> [{'type': 'image', 'base64': 'iVBORw0KGgo...'}]
```

The agent read the report correctly (HbA1c 6.1 %, triglycerides 3.4 mmol/L, both
matching the image) while `th_files.file_name` was already
`2026-08-23_Lab_Report_Patient_Demo1.png`.

Gates from CONTRIBUTING.md, on this branch:

```
python -m pytest -q     ->  197 passed in 10.96s
lint-imports            ->  Contracts: 2 kept, 0 broken.
```

## One thing left for a maintainer

The LLM rename itself is untouched — it is a feature, and the descriptive name is
what the file library should show. But a file attached to the current turn is now
reachable only under the request's name, while the UI shows it under the
generated one. If a user refers to the name they see on screen, the agent will
not find it by that name until the file has aged into `/library/`. Making the
mount answer to both names is a small change; I did not make it because it is a
product call about which name is canonical.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `85647b8c4d16`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.