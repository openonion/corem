---
name: co-rem
description: Set up REM, a local notebook of the user's people, projects and decisions, or answer questions from an existing notebook with sources. Use for "set up my memory", "remember my contacts and projects", "who is this person", or "where does this project stand". Explain source access and scheduling before starting setup.
---

# co rem

REM builds cited Markdown pages from the user's mail and coding sessions.
The ConnectOnion CLI runs locally and uses the configured coding agent or model
service to investigate sources. Pages stay on the user's computer.

Read every command's output, including its warnings and its `Next:` line, not
just the exit code. A command can succeed and still report a skipped step.

| Situation | Go to |
|---|---|
| Install the plugin or skill | Install only, then explain how to start setup |
| No notebook yet, or the user asks to set up memory | 1 Install → 2 Set up memory |
| A notebook exists and the user asks about a person, project or company | 3 Use |
| Something looks wrong (stale pages, upkeep not running) | 4 Check |

## 1. Install or update ConnectOnion

co rem needs **connectonion 1.9.3rc41 or later** (a preview). Find the
interpreter (`python3 --version`; on Windows `py -3 --version`) and the current
version (`co --version`), then update through whatever installed it:

```bash
pip install --upgrade --pre connectonion
# an existing uv tool install instead:
uv tool upgrade connectonion --prerelease allow
```

Compare versions with PEP 440 ordering, not alphabetically. Reuse an existing
compatible installation. Follow the host's permission flow when a command needs
network or home-directory access. Report a denied operation and the required
user action. Installation alone does not authorize source reading or setup.

## 2. Set up memory

```bash
co init
```

Before running initialization, read `co init --help`, `co rem init --help`,
and `co rem config --help`. Behavior varies between CLI releases.

In current releases, `co init` immediately grants access to local Codex and
Claude Code sessions and all connected Google/Microsoft mailboxes, starts the
first build, and installs upkeep. Mailboxes connected later may join automatically.
The CLI's cost estimate is informational and may not wait for an answer.
Do not depend on a terminal confirmation prompt.

Explain the sources that will be read, the configured runner/model, expected
quota use, the schedule, and any automatic task execution enabled by the CLI.
Ask the user to approve those effects unless their current instruction already
explicitly approves them. If they decline, stop. A request to install only is
not approval for setup.

For a narrower request, use the installed CLI's source and scheduling controls
before any reading. `co rem init --no-start` leaves a new background schedule
off, but does not stop an existing schedule. `co init --no-rem` skips REM while
preparing the CLI. Explain an unsupported restriction instead of running a
command that reads more than the user approved.

After approval, run the appropriate setup command, normally `co init`, in the
foreground. Let the user complete account authorization in their browser.
On versions that ask terminal questions, let the user answer source-consent
questions themselves. Report written pages, skipped stages, errors, and the
actual next step from the output. An interrupted build may keep completed pages.

Explain `co rem status` and `co rem stop` after setup. Read the installed help
before describing how to resume or rebuild an existing notebook.

## 3. Use the notebook

For a task that involves a person, project or company, read the relevant existing
page or search results. A missing notebook is a reason to offer setup, not to
start reading mail or sessions automatically. Pages have numbered sources.

```bash
co rem show "Mara Ostrowski"          # one person's page: where you stand, open threads, history
co rem search "data-sharing addendum"  # across every page
co rem list people                     # who is in the notebook
co rem open                            # read it in the browser, phone-friendly
```

Quote the page's wording and keep its citation numbers when you repeat a fact;
if a page says something is uncertain, say so too. When the notebook names
several people for one name, show them and let the user choose.

## 4. Check it

```bash
co rem status      # last run, next run, pages changed today, what is waiting on the user
co rem logs        # every run, with what it read and wrote
co rem sync        # update now from the latest mail and sessions
co rem stop        # pause upkeep; co rem start resumes it
```

`sync` reads subscribed sources and can make model calls. `stop` pauses future
scheduled updates and keeps existing pages. Before enabling upkeep with
`co rem start`, explain its current effects and follow the same approval rule
as setup. Source changes affect future reading; existing pages may remain.
`co rem --help` lists the installed version's other commands.
