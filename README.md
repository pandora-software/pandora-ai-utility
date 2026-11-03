<p align="center">
  <img src="docs/images/hero.svg" alt="Pandora coordinates Agent A and Agent B, whose work joins into one output." width="1280">
</p>

# Pandora

**Run Claude Code and Codex together in VS Code.**

Pandora gives your coding agents a shared place to talk, organise work and keep project notes. You can ask one agent to write a feature and another to review it, follow their progress, and inspect the changes without passing context between separate chats.

It uses the agent tools you're already signed in to. You don't need separate model API keys for this setup; your providers' usage limits and billing still apply.

> **In development · Not publicly available yet.** This repository is a preview of Pandora. The setup instructions below are for testers who already have a build.

[Chat](#team-chat) · [Tasks](#tasks-and-code-review) · [Workflows](#workflows) · [Knowledge](#project-knowledge) · [Usage and controls](#usage-and-controls) · [Tester setup](#tester-setup) · [Feedback](#feedback)

[![Pandora's task board, showing task owners and work moving through Todo, Doing, Review and Done.](docs/images/tasks.png)](docs/images/tasks.png)

## Team chat

Talk to `@claude`, `@codex` or `@all` in the same conversation. Messages without a mention go to Pandora, the coordinator. Agents can share updates and hand work to each other, while you follow along, answer questions or add a follow-up as they work.

```text
@all add a dark mode toggle, then review the changes and run the tests
```

[![An expanded Pandora chat view with agent replies, a question with clickable answers and live test output.](docs/images/chat.png)](docs/images/chat.png)

<details>
<summary><strong>Chat tools</strong></summary>

- Keep separate conversations with their own agent sessions. Rename, archive or delete chats as needed.
- Mention workspace files with autocomplete, open file links from replies, and attach files or images. Agents can send screenshots back.
- Answer questions with clickable choices. Edit or delete messages you've sent, or send a follow-up during an active turn.
- Choose each agent's model, effort level and access for each chat: **Read only**, **Edit** or **Shell**.
- Expand a turn to see its steps, command output, duration and exit status. Open changed files as before/after diffs.
- Undo a turn's changes, with a warning if a file has changed again. Inspect logs and retry failed turns.
- Collapse long exchanges between agents while keeping questions and final results visible.

[View an expanded turn](docs/images/turn.png) · [View the chat list](docs/images/chats.png)

</details>

## Tasks and code review

Open **Tasks** beside **Chats** and **Work** to use the full task board. Give work a clear brief, an owner and a checklist. Add dependencies and acceptance criteria so everyone can see what needs to happen before a task is done. Starting an assigned task sends the brief to its agent and moves the card to **Doing**.

You can review changed files in VS Code, leave line comments for the agent and open a GitHub pull request from the task. Merging stays with you.

<details>
<summary><strong>Task details and review tools</strong></summary>

[![A Pandora task with a description, checklist, acceptance criteria and review tools.](docs/images/task.png)](docs/images/task.png)

- Start with **Todo**, **Doing** and **Done**, or add columns such as **Review**. Reorder and recolour the board.
- Add owners, categories, tags, severity, images, checklists and dependencies to cards.
- Record passing evidence for acceptance criteria before an agent finishes a task.
- Create a task from chat: `/task @codex write tests for the parser`.
- Use mentions such as `@Todo` or `@bugs` to reach agents working on a group of tasks.
- Give a task its own Git branch, or use an optional worktree and port.
- Include the task's criteria and checks when opening a pull request. Follow its status from the card.
- Archive finished tasks so agents can still look up the work later.

</details>

## Workflows

Open **Flows** from the panel title bar to see your workflows and recent runs. Save a process you use often as a workflow. Connect steps for planning, coding, review and testing, then choose the agent and role for each one. Work can run in parallel, join back together and pause when it needs your input.

[![The workflow editor showing Studio Session: a coordinator, three parallel coders, a continuity checker and a tester.](docs/images/editor.png)](docs/images/editor.png)

Five workflows are included:

| Workflow | What it does |
| --- | --- |
| **Studio Session** | Plans a feature, splits implementation across agents, checks that the changes fit together and runs tests. |
| **Bug Fix** | Reproduces a problem, fixes the cause and checks the result. |
| **Optimize** | Measures a baseline, makes changes and measures again. |
| **Council** | Brings several models into a discussion and checks decisions with you. |
| **Update Knowledge** | Creates or refreshes the project's shared notes. |

<details>
<summary><strong>Workflow editor and controls</strong></summary>

- Drag steps into place and connect their outcomes. A **Join** step waits for parallel branches to finish.
- Set the agent, role, model, effort level and permissions for each step.
- Delegate a focused job to a helper model.
- Limit steps, loops and concurrent turns. Token budgets are optional.
- Start a workflow from the editor, the **Flows** title-bar button or chat: `/run studio add OAuth login`.

[View workflows and recent runs](docs/images/flows.png)

</details>

## Project knowledge

Decisions and findings shouldn't disappear into an old chat. Pandora keeps shared notes in `.pandora/knowledge`, where agents can find what has already been agreed, read the relevant context and update it as the project changes.

The notes are Markdown files you can read, edit and commit with your code. The graph lets you browse their connections and the source files they refer to.

[![Pandora's knowledge graph linking a project overview, plans, architectural notes and findings.](docs/images/graph.png)](docs/images/graph.png)

<details>
<summary><strong>Working with project notes</strong></summary>

- Keep decisions, plans, findings and how-tos together across conversations.
- Give agents a compact index and tools to find, read and update existing notes.
- Use coordination rules and edit hooks to keep new documentation in the shared knowledge folder.
- Search the graph, filter by note type, show referenced code files and open notes to read them.
- Commit the notes so they stay with the project.

</details>

## Usage and controls

The stats view shows where time and tokens are going. Compare agents, roles, models and effort levels, or look at individual runs to find slow commands and failed work.

The **Work** tab shows who's active and which files they've claimed. You can pause, resume or stop agents there, or stop an active turn directly from chat.

[![Pandora's stats dashboard showing token trends, agent time, role efficiency, commands and recent runs.](docs/images/stats.png)](docs/images/stats.png)

<details>
<summary><strong>Usage tracking and budgets</strong></summary>

- Track turns, fresh and cached input, output tokens and elapsed time.
- Compare success rates and average token use by agent, role, model and effort level.
- Separate command time, model time and other work. Inspect slow commands and recent runs.
- Set optional token budgets for tasks and workflows.

Missing usage is shown as **unknown**. An active turn can exceed its token budget before further work pauses, so budgets aren't hard spending caps. Token totals describe usage, not a dollar invoice.

</details>

<details>
<summary><strong>Coordination, permissions and recovery</strong></summary>

Pandora runs the agent CLIs in your workspace and gives them shared messages, tasks, file claims and notes. Claims and edit guards help agents avoid conflicting changes; build locks prevent overlapping builds in the same build tree.

- **Permissions:** choose access per chat. Codex uses its workspace sandbox; Claude uses a configured tool allowlist.
- **Run controls:** pause, resume or stop agents. Loop guards pause repeated exchanges between agents, and timeouts limit stalled work.
- **Health checks:** inspect hooks, commands, the runner, waiting messages and locks on demand. Repairs run only when you choose them.
- **Recovery:** the board is backed up daily. Export and restore are also available.
- **Project files:** `.pandora/` holds shared configuration and knowledge. Chats, tasks and runtime state are stored separately from your source files.

[![The Work tab showing agent status, tasks, health checks and claimed files.](docs/images/work.png)](docs/images/work.png)

</details>

## Tester setup

You'll need a test build supplied to you; Pandora isn't publicly available yet.

**Currently supported:** Claude Code and Codex. More agents are planned.

**Requirements:** VS Code, signed-in Claude Code and Codex tools, Node.js **22.13+**, and Git. Install the GitHub CLI (`gh`) if you want to open pull requests from tasks.

1. **Unzip your test build.** Use the package provided to you for testing.
2. **Install the extension.** Run `install.cmd` on Windows or `sh install.sh` on macOS/Linux, then reload VS Code.
3. **Set up your project.** Open Pandora from the activity bar and choose **Set up workspace**. Apply the Codex configuration snippet if one is shown.
4. **Enable the hooks.** Start a Codex chat once and approve Pandora's hooks when prompted.

A first message can be as simple as:

```text
@claude explain how this project is organised
```

When you're ready to try a workflow, use `/run studio <your feature>`.

## Feedback

Found a bug or something confusing? [Open an issue](https://github.com/pandora-software/pandora-ai-utility/issues) with what you tried, what you expected and what happened. Include your Pandora and VS Code versions.

Testers can also type `/report` in a Pandora chat. You choose what to include, then a debug report opens for you to read and edit. Reports are filtered to remove paths, email addresses, usernames and keys; chat text is included only if you select it. **Open Issue** submits the report using your own GitHub sign-in.

Issues in this repository are public, so review the report before posting.

---

<p align="center">
  <img src="docs/images/logo.svg" alt="" width="28"><br>
  <strong>Pandora Software</strong><br>
  <sub>© 2026 Pandora Software · <a href="LICENSE">All rights reserved</a></sub>
</p>
