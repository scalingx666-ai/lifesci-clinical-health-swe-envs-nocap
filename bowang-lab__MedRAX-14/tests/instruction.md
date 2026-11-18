# Issue

**Title:** enabling local llm

## Description

Enabling the use of local LLM frameworks such as [Ollama](https://ollama.com/) or [LM Studio](https://lmstudio.ai/).

- [x] Tested with LM Studio v0.3.10 ([chestagentbench](https://github.com/amarzullo24/MedRAX?tab=readme-ov-file#chestagentbench))
- [x] Updated docs
- [x] Updated README

If you are running a local LLM using frameworks like [Ollama](https://ollama.com/) or [LM Studio](https://lmstudio.ai/), you need to configure your environment variables accordingly. For example:
```
export OPENAI_BASE_URL="http://localhost:11434/v1"
export OPENAI_API_KEY="ollama"
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0483c15f687c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.