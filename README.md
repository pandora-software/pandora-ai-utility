<div align="center">

<img src="docs/images/logo.svg" alt="Pandora logo" width="96">

# Pandora

**AI agents that work as a team in your repo.**

A VS Code extension for Claude Code and Codex, using the subscriptions and models you already have.

<img src="https://img.shields.io/badge/VS%20Code-extension-2F8BFF" alt="VS Code extension">
<img src="https://img.shields.io/badge/works%20with-Claude%20Code%20%C2%B7%20Codex-7C5CFF" alt="Works with Claude Code and Codex">
<img src="https://img.shields.io/badge/platform-Windows%20%C2%B7%20macOS%20%C2%B7%20Linux-555" alt="Windows, macOS and Linux">
<img src="https://img.shields.io/badge/license-proprietary-555" alt="Proprietary license">

[**Install**](#install) · [Features](#features) · [Workflows](#team-workflows) · [FAQ](#faq) · [Releases](https://github.com/pandora-software/pandora-ai-utility/releases) · [Report a problem](https://github.com/pandora-software/pandora-ai-utility/issues)

<br>

<img src="docs/images/chat.png" alt="A chat where Claude adds a dark mode toggle, Codex reviews it, the task is marked done, and Claude asks a question" width="420">

</div>

<br>

Talk to Claude Code and Codex from one panel. They share your chats, claim files before they edit so they never overwrite each other, keep a shared knowledge base, track work on a task board, and can run as a whole team: one plans, several build in parallel, another tests.

**No API keys and no extra bill.** Pandora runs the Claude Code and Codex you're already signed in to.

## Highlights

<table>
<tr>
<td width="33%" valign="top">

**One chat, every agent**<br>`@claude`, `@codex` or `@all`, or just ask and let Pandora pick.

</td>
<td width="33%" valign="top">

**No collisions**<br>Agents claim files before editing, so no one overwrites anyone.

</td>
<td width="33%" valign="top">

**Undo any turn**<br>Live steps, before/after diffs and one-click undo.

</td>
</tr>
<tr>
<td valign="top">

**Task board with proof**<br>Tasks finish only after a passing check for each acceptance criterion.

</td>
<td valign="top">

**Team workflows**<br>Plan, build in parallel, review and test, as a flow you can draw.

</td>
<td valign="top">

**Shared knowledge**<br>Decisions and findings live as notes in your repo, for every chat.

</td>
</tr>
</table>

## How it works

```mermaid
flowchart LR
    you(["You"]) -->|chat| panel["Pandora panel"]
    panel -->|"@claude"| claude["Claude Code"]
    panel -->|"@codex"| codex["Codex"]
    claude <-->|"claims · tasks · notes · messages"| board[("Shared board<br>in your repo")]
    codex <-->|"claims · tasks · notes · messages"| board
```

Pandora runs the agent CLIs you already have, in your workspace, and gives them a shared board to coordinate through: file claims, a task list, a message inbox and a knowledge base.

## Features

### Chat with your agents

<table>
<tr>
<td width="58%" valign="top">

- **One chat, every agent.** Write `@claude`, `@codex` or `@all`. A message with no name goes to **Pandora**, a small coordinator that hands the work to the right agent.
- **Many chats.** Each chat keeps its own agent sessions, so context never leaks between them. Rename, archive or delete them.
- **Point at files.** `@src/app.js` autocompletes from your workspace. File names in replies become buttons that open the file.
- **Images.** Paste a screenshot, drop a file or click **+**. Agents can take screenshots of VS Code and attach them to replies.
- **Questions you click.** When an agent needs a decision, it asks with buttons, so you can answer in one click.
- **Edit and delete.** Fix a message after sending it, right where it is, and the agent gets the corrected text.
- **Messages arrive mid-turn.** A follow-up reaches an agent that's already working, without waiting for it to finish.
- **Models and permissions per chat.** Set each agent's model and effort, and choose Read only, Edit or Shell access.

</td>
<td width="42%" valign="top" align="center">

<img src="docs/images/chats.png" alt="The chat list with three chats and their latest replies" width="320">

</td>
</tr>
</table>

### See every step, undo any turn

<table>
<tr>
<td width="42%" valign="top" align="center">

<img src="docs/images/turn.png" alt="A finished turn opened up: its test command, six steps, three changed files and an Undo button" width="320">

</td>
<td width="58%" valign="top">

- **Live steps.** While an agent works, you see what it's reading and editing, with a **Stop** button.
- **Build and test cards.** Each command shows live: how long it's been running and what's running under it. When it finishes you get ✓ or ✗, the time and exit code, and the end of its output.
- **Diffs.** Every changed file opens as a before/after diff.
- **Undo.** One click puts back everything a turn changed. It warns you if a file changed again afterwards.
- **Retry and logs.** A failed turn shows why, with **Retry** and **Log**.
- **Quiet teamwork.** Long back-and-forths between agents fold into one line, such as "Codex and Claude worked together · 2m 26s". Questions for you and final results are never folded.

</td>
</tr>
</table>

### No collisions

<table>
<tr>
<td width="58%" valign="top">

- **File claims.** An agent claims a file before editing it. Another agent is blocked from it until it's released, so no one overwrites anyone's work.
- **Work tab.** See who's ready or working, pause or stop an agent, and see which files are in use and why.
- **Health check.** **Run health check** looks at hooks, commands, the background runner, waiting mail and locks. It only reads; repairs run when you choose them.
- **Own worktree per task (optional).** A task can get its own Git worktree and port, so agents can work on several tasks side by side.

</td>
<td width="42%" valign="top" align="center">

<img src="docs/images/work.png" alt="The Work tab: agent status with Pause buttons, open tasks and the files each agent is editing" width="320">

</td>
</tr>
</table>

### Task board

<img src="docs/images/tasks.png" alt="The task board with Todo, Doing, Review and Done lists, tags, severity, checklists and owners" width="100%">

- **Lists.** Todo, Doing and Done are built in. Add your own (like Review), and recolour or reorder them.
- **Cards.** Each card has an owner, a category, coloured tags, a severity, a checklist, images and dependencies.
- **Start when you say.** A new task waits in Todo even when it's assigned. **Start** sends the brief to its owner and moves the card to Doing.
- **Proof of done.** Give a task acceptance criteria. An agent can only finish it after recording a passing check for each one.
- **From chat.** `/task @codex write tests for the parser` adds a task. `@Todo` or `@bugs` messages everyone working on those tasks.
- **Archive.** Clear finished work off the board and still let agents look it up later.

<details>
<summary><b>See an open task card</b></summary>
<br>
<p align="center">
  <img src="docs/images/task.png" alt="An open task card with its description, a half-done checklist and three acceptance criteria" width="720">
</p>
</details>

### Branches, review and pull requests

- **A branch per task.** Each task can get its own branch, and the brief tells the agent to commit there.
- **Review in VS Code.** **Review changes** opens each changed file as a diff. Comment on a line, and the comment goes straight to the agent that owns the task.
- **Pull requests.** **Open pull request** pushes the branch and opens a PR on GitHub with the task, its criteria and its checks. The card then shows the PR's status and checks. Merging stays with you.

## Team workflows

<img src="docs/images/editor.png" alt="The workflow editor showing Studio Session: a coordinator, three coders in parallel, a continuity checker and a tester" width="100%">

Pick a flow, describe the job, and watch the team work. Steps run in parallel, wait for each other, and stop to ask you when a decision is yours.

| Flow | What it does |
|---|---|
| **Studio Session** | Builds a feature end to end: planned in phases, developed in parallel by three coders, checked for continuity, and tested until it's done. |
| **Bug Fix** | Reproduces a bug, fixes the cause and confirms the fix. |
| **Optimize** | Measures, improves and re-measures in a loop until a goal is met, such as 30 → 60 fps. |
| **Council** | Several models plan an idea together and check key decisions with you. |
| **Update Knowledge** | Brings the knowledge base up to date with the code, or builds one from scratch. |

<table>
<tr>
<td width="58%" valign="top">

- **Draw your own.** Drag steps, connect them by outcome, and mark a step **Join** to wait for parallel branches.
- **Roles.** Each step is one agent in one role (Coordinator, Coder, Tester, Reviewer and more), with its own model, effort and permissions.
- **Helpers.** Any step can hand small jobs, like running a benchmark or summarising files, to a cheap, fast helper model.
- **Limits.** Cap the number of steps, loops and parallel turns, and optionally the tokens a run may use.
- **Start anywhere.** Type `/run studio add OAuth login` in chat, or use **Run** in the editor or the Flows tab.

</td>
<td width="42%" valign="top" align="center">

<img src="docs/images/flows.png" alt="The Flows tab listing the five workflows and a finished Studio Session run" width="320">

</td>
</tr>
</table>

## Shared knowledge base

<img src="docs/images/graph.png" alt="The knowledge graph: notes coloured by kind, growing as a tree from the overview and plan" width="100%">

- **Notes in your repo.** Agents write decisions, plans, findings and how-tos as Markdown notes in `.pandora/knowledge`. Commit them, and the knowledge travels with your code.
- **Every chat starts informed.** Each turn sees the list of notes, so agents update a note instead of writing a duplicate.
- **No stray files.** Agents can't scatter new Markdown files around your repo. Notes go in one place.
- **The graph.** A live map of every note, coloured by kind and growing from the plan. Search, filter by kind, show the code files notes mention, and click a note to read it.

## Stats and budgets

<img src="docs/images/stats.png" alt="Pandora stats: turns, tokens, agent time, commands and files, tokens per day, time per agent, and efficiency by role and model" width="100%">

- **What it costs.** Turns, tokens (fresh, cached and output) and time, per day, per agent, per role and per model.
- **Where time goes.** Commands like builds and tests, the model, and everything else.
- **What's worth running.** Success rate and average tokens by role, model and effort, plus the slowest commands and recent workflow runs.
- **Token budgets.** Optionally cap the tokens a task or a workflow run may use. Capped work pauses, and nothing is guessed.

## Safety and control

<table>
<tr>
<td width="50%" valign="top">

**Agents stay in your project**<br>Codex runs in its workspace sandbox, and Claude runs with a fixed list of allowed tools.

</td>
<td width="50%" valign="top">

**Loop guard**<br>If agents keep waking each other without you, Pandora pauses them and tells you. Turns time out after 30 minutes.

</td>
</tr>
<tr>
<td valign="top">

**You're in charge**<br>Pause, resume or stop any agent from the Work tab.

</td>
<td valign="top">

**Backups**<br>The board is backed up daily, and you can export and restore it at any time.

</td>
</tr>
<tr>
<td colspan="2" valign="top">

**A clean repo**<br>Setup adds a single `.pandora/` folder to your project. Everything else lives in your user settings.

</td>
</tr>
</table>

## Install

| Requirement | Details |
|---|---|
| **VS Code** | with the **Claude Code** and **Codex** extensions installed and signed in |
| **Node.js** | 22.13 or newer |
| **git** | any recent version |
| **GitHub CLI** (`gh`) | optional, only if you want Pandora to open pull requests |

1. Download `pandora-<version>.zip` from [Releases](https://github.com/pandora-software/pandora-ai-utility/releases) and unzip it.
2. Run `install.cmd` (Windows) or `sh install.sh` (macOS/Linux), then reload VS Code.
3. Open a project, click the **Pandora** icon in the activity bar, and choose **Set up workspace**. If the panel then shows a snippet for `~/.codex/config.toml`, copy it in.
4. Start a Codex chat once, and approve Pandora's hooks when it asks.

Then type in the panel:

```text
@all add a dark mode toggle
```

or start a whole team with `/run studio <your feature>`.

## FAQ

<details>
<summary><b>Does it cost anything extra?</b></summary>
<br>
No API keys and no extra bill. Pandora runs the Claude Code and Codex you're already signed in to, so usage counts against the subscriptions you already have.
</details>

<details>
<summary><b>Which agents does it support?</b></summary>
<br>
Claude Code and Codex, side by side in the same chats.
</details>

<details>
<summary><b>What does it add to my project?</b></summary>
<br>
One <code>.pandora/</code> folder, which holds the knowledge base. The task board, chats and settings live outside your source files.
</details>

<details>
<summary><b>Can I stop the agents?</b></summary>
<br>
Yes. Every turn has a <b>Stop</b> button, and the Work tab lets you pause, resume or stop any agent. The loop guard also pauses agents that keep waking each other without you.
</details>

## Report a problem

Open an [issue](https://github.com/pandora-software/pandora-ai-utility/issues) with what you did, what you expected and what happened. Include your Pandora and VS Code versions.

Pandora can save a debug report of a chat: type `/getfeedback` in it. The report contains your chat text, commands and logs. **Read it before attaching it**, because issues here are public.

## License

Copyright © 2026 Pandora Software. All rights reserved. See [LICENSE](LICENSE).

Pandora is proprietary software. This repository holds documentation and release builds only.

<br>

<div align="center">
<sub>Screenshots show a made-up demo project.</sub>
</div>
