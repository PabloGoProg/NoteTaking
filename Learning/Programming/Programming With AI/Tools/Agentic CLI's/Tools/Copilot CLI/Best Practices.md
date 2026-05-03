---
tags:
  - AI-Tools
  - Github
sources:
  - "[Copilot CLI Docs](https://docs.github.com/en/copilot/how-tos/copilot-cli)"
---
### Custom Instructions Files

`Repository instruction > Global Instructions` -> 

| Location                                    | Scope                 |
| ------------------------------------------- | --------------------- |
| `~/.copilot/copilot-instructions.md`        | All sessions (global) |
| `.github/copilot-instructions.md`           | Repository            |
| `.github/instructions/**/*.instructions.md` | Repository (modular)  |
| `AGENTS.md` (in Git root or cwd)            | Repository            |
| `Copilot.md`, `GEMINI.md`, `CODEX.md`       | Repository            |
