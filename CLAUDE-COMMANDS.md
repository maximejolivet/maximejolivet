# CLAUDE CODE COMMANDS

Reference for Claude Code commands, with examples. Checked against Claude Code 2.1.327 (November 2026). For the full, up-to-date list, type `/help` in a session or read the [official commands reference](https://code.claude.com/docs/en/commands).

---

## SLASH COMMANDS (inside a session)

These are typed in the Claude Code prompt, starting with `/`.

### `/help`

Shows help and the list of available commands. Pass a command name to see its usage.

```
> /help
> /help compact
```

### `/clear`

Starts a new conversation with empty context. Use it when switching to an unrelated task, so old context does not pollute new answers. Aliases: `/reset`, `/new`.

```
> /clear
> /clear auth-refactor
```

The optional name labels the previous conversation in the `/resume` picker.

### `/compact`

Summarizes the conversation to free up context space, without erasing it. Use it on a long session that still needs its history.

```
> /compact
> /compact keep only the decisions about authentication
```

Anything after `/compact` is used as instructions for the summary.

### `/resume`

Reopens a previous session by ID or name, or from a list, so you can continue where you stopped.

```
> /resume
> /resume auth-refactor
```

### `/rename`

Renames the current session, so it is easy to find in `/resume`. Without a name, Claude generates one.

```
> /rename auth-refactor
```

### `/rewind`

Returns the conversation, the code or both to an earlier point. Aliases: `/checkpoint`, `/undo`.

```
> /rewind
```

### `/branch`

Creates a branch of the conversation at this point, to try another direction without losing the current one.

```
> /branch try-redis-cache
```

### `/btw`

Asks a side question about the session without adding it to the conversation.

```
> /btw which file holds the database configuration?
```

### `/model`

Switches the model and saves it as your default for new sessions. In the picker, press `s` on a row to switch for the current session only.

```
> /model
> /model fable
> /model opus
> /model sonnet
> /model haiku
```

Use a larger model for hard reasoning and a smaller one for quick, simple tasks.

### `/effort`

Sets how much effort the model puts into its work.

```
> /effort high
> /effort auto
> /effort status
```

Levels go from `low` to `xhigh`, then `max`. Available levels depend on the model.

### `/fast`

Turns fast mode on or off.

```
> /fast on
> /fast off
```

### `/plan`

Enters plan mode, where Claude proposes a plan before changing anything.

```
> /plan
> /plan migrate the API to Symfony 8
```

### `/goal`

Sets a condition. Claude keeps working across turns until it is met.

```
> /goal all tests in the api folder pass
> /goal clear
```

### `/background`

Detaches the session to run as a background agent, which frees the terminal.

```
> /background
> /background then open a draft pull request
```

### `/tasks`

Shows and manages the background work of the current session, such as shells and subagents.

```
> /tasks
```

### `/diff`

Reviews the changes in the working tree, including the edits Claude has made so far.

```
> /diff
```

### `/config`

Opens the settings screen (theme, verbosity, defaults and so on). Pass `key=value` to change a setting directly.

```
> /config
> /config theme=dark
```

### `/permissions`

Shows and edits which tools Claude can use without asking. Useful to allow a command you run often, such as tests.

```
> /permissions
```

In the list, you can add a rule such as `Bash(npm run test:*)` to allow test commands without a prompt each time.

### `/memory`

Edits the memory files (CLAUDE.md) that Claude reads at the start of each session, and manages auto memory. Use it to store project rules, such as "always use pnpm" or "answer in French".

```
> /memory
```

### `/init`

Analyzes the project and creates a CLAUDE.md file describing its structure, commands and conventions.

```
> /init
```

Run it once at the root of a new project.

### `/import`

Brings configuration from OpenAI Codex, Gemini CLI or Cursor into Claude Code.

```
> /import codex --dry-run
```

### `/agents`

Reminds you how to create subagents: ask Claude directly, or edit `.claude/agents/` or `~/.claude/agents/`. For example, a "security reviewer" agent that only reads code.

```
> /agents
```

### `/skills`

Lists the available skills, with a filter by name, description or source.

```
> /skills
```

### `/plugin`

Manages Claude Code plugins: browse, install, enable or remove them.

```
> /plugin
> /plugin list
```

### `/mcp`

Shows the connected MCP servers (external tools and services) and their status. Use it to check that an integration is working, to authenticate it or to reconnect it.

```
> /mcp
> /mcp reconnect all
```

### `/hooks`

Shows the configured hooks: shell commands that run automatically on events, such as after each file edit.

```
> /hooks
```

Example use: run a linter every time Claude edits a `.ts` file.

### `/add-dir`

Adds a folder to the session, so Claude can read and edit files there too. Useful when a project spans several folders.

```
> /add-dir ~/Sites/my-other-project
```

### `/cd`

Moves the session to another working directory and keeps the conversation.

```
> /cd ~/Sites/my-other-project
```

### `/context`

Shows how much of the context window is used and what takes up space. Use it when answers start to degrade in a long session.

```
> /context
```

### `/usage`

Shows the session cost, plan usage limits and activity stats. `/cost` and `/stats` are aliases.

```
> /usage
```

### `/insights`

Generates an HTML report on how you use Claude Code across your recent sessions.

```
> /insights
```

### `/status`

Opens the Status tab of the settings: version, model, account and connectivity.

```
> /status
```

### `/doctor`

Runs a setup checkup of the installation, settings, extensions and CLAUDE.md files, then proposes fixes that Claude applies after you confirm. Alias: `/checkup`.

```
> /doctor
```

### `/ide`

Connects Claude Code to your IDE (for example VS Code), so it can see the open file and the selection.

```
> /ide
```

### `/sandbox`

Turns sandbox mode on or off, on supported platforms.

```
> /sandbox
```

### `/remote-control`

Makes the session available from claude.ai or the Claude app, so you can follow it from another device.

```
> /remote-control
```

### `/teleport`

Pulls a cloud session into this terminal, with its branch and conversation. Alias: `/tp`.

```
> /teleport
```

### `/export` and `/copy`

`/export` saves the conversation as plain text. `/copy` copies the last response to the clipboard, or the Nth-latest one.

```
> /export session-notes.txt
> /copy
> /copy 2
```

### `/release-notes`

Shows the changelog in a version picker.

```
> /release-notes
```

### `/login` and `/logout`

Log in to or out of your Anthropic account.

```
> /login
> /logout
```

### `/exit`

Quits Claude Code. Alias: `/quit`.

```
> /exit
```

### REVIEW, VERIFICATION AND AUTOMATION

#### `/code-review`

Reviews the current diff, or a given PR, branch or path, and reports likely bugs. `/review` is an alias.

```
> /code-review
> /code-review 42
> /code-review high --fix
> /code-review 42 --comment
```

`42` is an example PR number. `--fix` applies the findings and `--comment` posts them on the PR.

#### `/ultrareview`

Runs a deep, multi-agent code review in a cloud sandbox.

```
> /ultrareview
> /ultrareview 42
```

#### `/security-review`

Security review of the changes on the current branch: injections, auth issues, data exposure.

```
> /security-review
```

#### `/simplify`

Reviews the modified code and applies cleanups: reuse, simpler logic, better performance. It does not hunt for bugs; use `/code-review` for that.

```
> /simplify
> /simplify src/components
```

#### `/run` and `/verify`

`/run` launches and drives your app to see a change working. `/verify` builds and runs the app to confirm that a change does what it should.

```
> /run
> /verify
```

#### `/debug`

Turns on debug logging for the session and troubleshoots issues from the log.

```
> /debug the MCP server does not start
```

#### `/batch`

Orchestrates a large change across the codebase, with work split and run in parallel.

```
> /batch replace moment.js with date-fns across the project
```

#### `/deep-research`

Searches the web, cross-checks sources and writes a cited report.

```
> /deep-research compare Vue and Svelte for a mobile-first app
```

#### `/fewer-permission-prompts`

Scans your past sessions for common read-only commands and adds an allowlist to the project settings.

```
> /fewer-permission-prompts
```

#### `/loop`

Runs a prompt or command again at a fixed interval while the session stays open. Useful to watch something.

```
> /loop 5m check whether the deployment has finished
> /loop 10m /code-review
```

`5m` and `10m` are intervals. Without an interval, Claude chooses the pace itself.

#### `/schedule`

Creates a scheduled cloud task (formerly routines) that runs on a cron schedule, or once at a given time. Alias: `/routines`.

```
> /schedule every Monday at 9am, summarize open PRs
> /schedule tomorrow at 3pm, remind me to check the production release
```

### REMOVED COMMANDS

| Command | Replacement |
| --- | --- |
| `/vim` | `/config`, then Editor mode |
| `/pr-comments` | Ask Claude directly to read the PR comments |
| `/ultraplan` | Plan mode, with `/plan` or `Shift+Tab` |

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
claude -p "list the TODOs" --output-format json
claude -p --max-turns 3 --max-budget-usd 5 "fix the type errors"
```

`--max-turns` and `--max-budget-usd` limit a run in this mode.

### `claude -c`

Resumes the most recent conversation in the current folder.

```bash
claude -c
```

### `claude -r`

Resumes a session by ID or name, or opens a picker to choose one.

```bash
claude -r
claude -r "auth-refactor" "finish this PR"
```

### `claude -n`

Names the session, so you can find and resume it later.

```bash
claude -n "auth-refactor"
```

### `claude -w`

Starts Claude in an isolated git worktree, under `.claude/worktrees/`. Useful to run several tasks in parallel.

```bash
claude -w feature-auth
```

### Session options

Set the model, effort, permission mode or extra folders at startup.

```bash
claude --model sonnet
claude --effort high
claude --permission-mode plan
claude --add-dir ../my-other-project
```

### `claude --bg`

Starts a session as a background agent and returns immediately.

```bash
claude --bg "run the test suite and fix the failures"
```

### `claude agents`

Opens the agent view, to monitor and dispatch parallel background sessions.

```bash
claude agents
```

### Background session commands

Attach to a background session, read its output, stop it, restart it or remove it from the list.

```bash
claude attach 7c5dcf5d
claude logs 7c5dcf5d
claude stop 7c5dcf5d
claude respawn 7c5dcf5d
claude rm 7c5dcf5d
```

`7c5dcf5d` is an example session ID.

### `claude update`

Updates Claude Code to the latest version.

```bash
claude update
```

### `claude install`

Installs or reinstalls the native binary, at a given version or channel.

```bash
claude install stable
claude install latest
```

### `claude auth`

Signs in or out, or shows the authentication status, from the terminal.

```bash
claude auth login
claude auth status --text
claude auth logout
```

### `claude mcp`

Manages MCP servers from the terminal. For example, lists them, adds one or runs its OAuth flow.

```bash
claude mcp list
claude mcp add my-server -- npx -y my-mcp-package
claude mcp login my-server
```

To keep tokens off the command line, `claude mcp add-json <name> -` reads the server's JSON from stdin.

### `claude plugin`

Manages plugins from the terminal. Alias: `claude plugins`.

```bash
claude plugin install code-review@claude-plugins-official
```

### `claude remote-control`

Starts a Remote Control server, to control Claude Code from claude.ai or the Claude app. Alias: `claude rc`.

```bash
claude remote-control
```

### `claude import`

Starts a session that brings configuration from other coding agents into Claude Code.

```bash
claude import codex --dry-run
```

### `claude ultrareview`

Runs an ultrareview without an interactive session and prints the findings. Useful in CI.

```bash
claude ultrareview 42 --json
```

### `claude setup-token`

Generates a long-lived OAuth token for CI and scripts. It requires a Claude subscription.

```bash
claude setup-token
```

### `claude doctor`

Prints read-only diagnostics of the installation and settings, without starting a session.

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

Adds a file to the context of your question, with path autocomplete.

```
> explain this component @src/components/Header.tsx
```

### `Shift+Tab`

Switches the permission mode: `default` (Manual), `acceptEdits` and `plan`, then `bypassPermissions` and `auto` where available.

```
[Shift+Tab] → auto-accept edits mode
```

### `Esc`

Interrupts the current response, for example when Claude goes in the wrong direction. The work done so far is kept.

### `Esc Esc`

With text in the prompt, clears the draft. With an empty prompt, opens rewind, to return to an earlier point in the conversation and retry from there.

### Keyboard shortcuts

| Shortcut | Action |
| --- | --- |
| `?` | Show the shortcut help, on an empty prompt |
| `Ctrl+B` | Send running Bash commands and agents to the background |
| `Ctrl+G` | Edit the prompt in your default text editor |
| `Ctrl+L` | Redraw the screen |
| `Ctrl+O` | Open the transcript viewer, with tool details |
| `Ctrl+R` | Search the command history |
| `Ctrl+S` | Stash the prompt, or restore it |
| `Ctrl+T` | Show or hide Claude's task checklist |
| `Option+P` / `Alt+P` | Switch model without clearing the prompt |
| `Option+O` / `Alt+O` | Turn fast mode on or off |

On macOS, some `Option` shortcuts require setting Option as Meta in your terminal.
