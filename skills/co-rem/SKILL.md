---
name: co-rem
description: Set up co rem, a local notebook built from the user's mail and coding sessions, and read it before starting work. Use when the user asks to set up memory, co rem, "remember my contacts and projects", or asks who someone is, where a project stands, or what was agreed with a company. Setup reads private sources only after the user's own yes.
---

# co rem

co rem turns the user's Gmail or Outlook and their Codex and Claude Code sessions
into one cited Markdown page per person, project, organisation and skill, kept
on their machine and updated on a schedule they approved.

Read every command's output, including its warnings and its `Next:` line, not
just the exit code. A command can succeed and still report a skipped step.

| Situation | Go to |
|---|---|
| No notebook yet, or the user asks to set up memory | 1 Install → 2 `co init` |
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

Compare versions with PEP 440 ordering, not alphabetically. In Codex, run
installs, logins and `co init` outside the sandbox (escalated) from the first
try: they need the network and the user's real home directory.

## 2. Set it up: one command

```bash
co init
```

Run it in the user's terminal, not in the background: it asks questions only the
user can answer. In order, it:

1. writes the local identity and links the bundled skills (no questions);
2. offers `co auth google` or `co auth microsoft` when no mailbox is connected
   (the user may skip; without mail the notebook is built from coding sessions);
3. shows exactly which sources will be read, with which model, on which
   schedule and under which daily cap, and asks once:
   `Read these sources with this model and schedule? [y/N]`.
   **Only the user answers this.** Never type `y` for them, and never pass
   `--yes` to grant it. If they decline, setup ends cleanly and upkeep stays off;
4. installs upkeep (a Codex Scheduled task, or launchd on macOS without Codex)
   and names which one;
5. maps the last 180 days and prints an estimate (pages, tokens, minutes), then
   asks `Build the first map now? [Y/n]`. Enter builds; `n` keeps upkeep and
   prints `co rem init` for later.

Then the first pages arrive one by one. The user's own page comes first, within
minutes; a busy mailbox takes an hour or two in all, and every page is readable
as soon as it lands. Ctrl-C keeps what was written.

Re-running `co init` on a machine that already has a notebook changes nothing
and says so. `co init --no-rem` skips this step.

## 3. Use the notebook

Before starting a task that involves a person, a project or a company, read
their page first. Pages are plain Markdown with numbered sources.

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

If `status` shows no scheduled run, `co rem start` reinstalls upkeep after
showing the same consent summary. `co rem --help` lists everything else.
