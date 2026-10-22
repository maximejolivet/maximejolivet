# CLAUDE CODE COMMANDS

Reference for Claude Code commands, with examples. For the full, up-to-date list, type `/help` in a session.

---

## SLASH COMMANDS (inside a session)

These are typed in the Claude Code prompt, starting with `/`.

### `/help`

Shows help and the list of available commands.

```
> /help
```

### `/clear`

Clears the current conversation. Use it when switching to an unrelated task, so old context does not pollute new answers.

```
> /clear
```

### `/compact`

Summarizes the conversation to free up context space, without erasing it. Use it on a long session that still needs its history.

```
> /compact
> /compact keep only the decisions about authentication
```

Anything after `/compact` is used as instructions for the summary.

### `/resume`

Reopens a previous session from a list, so you can continue where you stopped.

```
> /resume
```

### `/model`

Switches the model for the rest of the session.

```
> /model
> /model opus
> /model sonnet
> /model haiku
```

Use a larger model for hard reasoning and a smaller one for quick, simple tasks.

### `/config`

Opens the settings screen (theme, verbosity, defaults and so on).

```
> /config
```

### `/permissions`

Shows and edits which tools Claude can use without asking. Useful to allow a command you run often, such as tests.

```
> /permissions
```

In the list, you can add a rule such as `Bash(npm run test:*)` to allow test commands without a prompt each time.

### `/memory`

Opens the memory files (CLAUDE.md) that Claude reads at the start of each session. Use it to store project rules, such as "always use pnpm" or "answer in French".

```
> /memory
```

### `/init`

Analyzes the project and creates a CLAUDE.md file describing its structure, commands and conventions.

```
> /init
```

Run it once at the root of a new project.

### `/agents`

Creates and manages specialized subagents, each with its own role and tools. For example, a "security reviewer" agent that only reads code.

```
> /agents
```

### `/mcp`

Shows the connected MCP servers (external tools and services) and their status. Use it to check that an integration is working or to authenticate it.

```
> /mcp
```

### `/hooks`

Configures hooks: shell commands that run automatically on events, such as after each file edit.

```
> /hooks
```

Example use: run a linter every time Claude edits a `.ts` file.

### `/add-dir`

Adds a folder to the session, so Claude can read and edit files there too. Useful when a project spans several folders.

```
> /add-dir ~/Sites/my-other-project
```

### `/context`

Shows how much of the context window is used and what takes up space. Use it when answers start to degrade in a long session.

```
> /context
```

### `/cost`

Shows the cost and duration of the current session.

```
> /cost
```

### `/status`

Shows the session state: model, account, working directory and active settings.

```
> /status
```

### `/doctor`

Checks the installation: version, configuration and connectivity. Run it when Claude Code misbehaves.

```
> /doctor
```

### `/ide`

Connects Claude Code to your IDE (for example VS Code), so it can see the open file and the selection.

```
> /ide
```

### `/login` and `/logout`

Log in to or out of your Anthropic account.

```
> /login
> /logout
```

### `/exit`

Quits Claude Code.

```
> /exit
```

### COMMANDS INSTALLED ON THIS MACHINE (skills)

#### `/code-review`

Reviews the current diff, or a given PR, and reports likely bugs.

```
> /code-review
> /code-review 42
```

`42` is an example PR number.

#### `/security-review`

Security review of the changes on the current branch: injections, secrets, unsafe inputs.

```
> /security-review
```

#### `/simplify`

Reviews the modified code and applies cleanups: reuse, simpler logic, better performance. It does not hunt for bugs; use `/code-review` for that.

```
> /simplify
```

#### `/loop`

Runs a prompt or command again at a fixed interval. Useful to watch something.

```
> /loop 5m check whether the deployment has finished
> /loop 10m /code-review
```

`5m` and `10m` are intervals. Without an interval, Claude chooses the pace itself.

#### `/schedule`

Creates a scheduled cloud agent (routine) that runs on a cron schedule, or once at a given time.

```
> /schedule every Monday at 9am, summarize open PRs
> /schedule tomorrow at 3pm, remind me to check the production release
```

---

## TERMINAL COMMANDS (outside a session)

These are run directly in the shell.

### `claude`

Starts an interactive session in the current folder.

```bash
cd ~/Sites/maximejolivet
claude
```

### `claude "question"`

Starts a session with a first message already sent.

```bash
claude "explain the architecture of this project"
```

### `claude -p "question"`

Non-interactive mode: prints the answer and exits. Ideal in scripts and pipes.

```bash
claude -p "summarize this file in three points" < README.md
git diff | claude -p "write a commit message for these changes"
```

### `claude -c`

Resumes the most recent conversation in the current folder.

```bash
claude -c
```

### `claude -r`

Opens a picker to choose a previous session to resume.

```bash
claude -r
```

### `claude update`

Updates Claude Code to the latest version.

```bash
claude update
```

### `claude mcp`

Manages MCP servers from the terminal. For example, lists them or adds one.

```bash
claude mcp list
claude mcp add my-server -- npx -y my-mcp-package
```

### `claude doctor`

Diagnoses the installation.

```bash
claude doctor
```

---

## USEFUL SHORTCUTS

### `!command`

Runs a shell command inside the session. The output is added to the conversation, so Claude can use it.

```
> !git status
> !npm run test
```

### `@file`

Adds a file to the context of your question, without copying its content.

```
> explain this component @src/components/Header.tsx
```

### `Shift+Tab`

Switches the permission mode: ask before each action, auto-accept edits, or plan only.

```
[Shift+Tab] → auto-accept edits mode
```

### `Esc`

Interrupts the current response, for example when Claude goes in the wrong direction.

### `Esc Esc`

Opens rewind, to return to an earlier point in the conversation and retry from there.
