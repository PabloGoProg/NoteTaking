An Agentic CLI is a Command Line Interface that has an AI Agent inside.
### CLI Common Agentic Loop

![](https://mintcdn.com/claude-code/c5r9_6tjPMzFdDDT/images/agentic-loop.svg?w=1650&fit=max&auto=format&n=c5r9_6tjPMzFdDDT&q=85&s=af82455f790bfd3de42cb85faeca38e7)

Three phases triggered by a user prompt: **Gather Context, Take Action and Verify Results** -> The agent can use tools throughout, whether searching files to understand your code, editing to make changes, or running tests to check its work.

- _The loops adapts to the prompt:_ The agent decides what each step requires based on the precious step. chaining `n` actions together and correcting the course along the way.
- _The user as part of the loop:_ The user can interrupt the process at any point. -> Providing additional context or make course suggestions are common cases for this.
- _Model-Tool Power:_ The models ([[LLM]]) reason and tools execute. -> The agent provides the tools, context management and execution environment.

---
### What Can The Agent Access?

- _Project Context_: Files and subdirectories in the executed directory. plus files elsewhere you give permissions.
- _Terminal_: Access to run any command you can execute.
- _Git State_: Current branch, uncommitted changes, and recent commit history.
- _{AGENT}.md_: Most CLI Providers creates or let the user create an _{AGENT}.md_ file (e.g. CLAUDE.md, GEMINI.md, etc.) to store project-specific instructions, conventions, and context.
- _Agent Extensions_: Skills, MCP Servers, Subagents, Hooks, etc.

---
### Execution Environments and Interfaces

An Agent can run in different environments, the most common for almost any agent are:

1. **Local** -> 	Default. Full access to your files, tools, and local environment.
2. **Cloud** -> Offload tasks, work on repos you don’t have locally.

Environments tells us where the agent is executed, interfaces says _how_. Many agents can be executed from a desktop app, an IDE extension, CI/CD Pipelines or the CLI itself.

---
### Sessions

Each conversation is a _session_ -> Each message, tool use and result are stored locally, and the agent commonly save snapshots of edited code in case revert is needed. 

- Each session start with fresh context -> Only accessing Agent Memory (Memory of User Preferences) and _{AGENT}.md_ file.
- Sessions are tied to the working directory (project),
- We can run parallel sessions of the same directory using different git branches.

**Resume and Forks** 
	-> Each session has an ID, every time we resume a session, we pick it up where it were left off, appending messages to the same conversation. (The store of scoped permissions depends of provider).
	-> To try a different approach without affecting the original session use forks (ideal method for same session. over different CLIs).

**Context Window on Sessions**
	The agent saves your conversation history, file contents, command outputs, _{AGENT}.md_, preferences memory, loaded skills and system instructions. -> Most agents compact context when it gets filled up, but early instructions could get lost.


