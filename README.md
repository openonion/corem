# co rem

**Your mail and coding sessions, turned into a notebook your AI agents can read.**

co rem reads the last 180 days of your Gmail or Outlook and your local Codex and Claude Code sessions. It writes one cited Markdown page for:
- each person you work with;
- each project you code in;
- each organisation you deal with;
- each skill you have installed.

The pages stay on your machine. Every sentence links back to the message it came from.

Your agents then use those pages, through a skill, before they start the next task.

<p align="center">
  <img src="assets/person-page-desktop.png" width="68%" alt="A person page in co rem: where you stand, contact details, activity and a cited history">
  <img src="assets/person-page-phone.png" width="24%" alt="The same page on a phone">
</p>
<p align="center"><sub>An invented example notebook. Your own pages are written from your own mail.</sub></p>

## Start in three commands

```bash
pip install --upgrade connectonion
co auth google          # or: co auth microsoft
co rem init             # map 180 days, then write your pages
co rem open             # read them in your browser
```

`init` prints your own page within the first minutes, then writes the rest 16 pages at a time on your own Claude Code or Codex plan. A full first run over a busy mailbox takes about two hours, and every page is readable as soon as it lands.

## What you get

| Page | What it answers |
|---|---|
| **You** | What you are working on now, who you write to most, what you owe |
| **People** | Who they are, how you know them, what is open between you, dated history |
| **Projects** | Where the work stands, what changed, which sessions moved it |
| **Organisations** | Who you know there, the terms you agreed, what is still open |
| **Skills** | What each installed skill does, how often it ran, how reliable it was |

Each page has an **Open threads** section that says who owes whom, a dated **History**, and **Sources** you can open as the original message.

## The skills

co rem is built from plain `SKILL.md` files, the same format Claude Code and Codex load. Two of them are for you.

### `rem-use`: let your agent read your notebook

Copy it from this repository into your agent's skills folder:

```bash
git clone https://github.com/openonion/corem
cp -r corem/skills/rem-use ~/.claude/skills/     # Claude Code
cp -r corem/skills/rem-use ~/.codex/skills/      # Codex
```

Then ask in plain words:

> "What did I promise Priya last week?"
> "Who at Fernhill have I spoken to, and what's still open?"
> "Which of my skills have actually been used this month?"

The agent answers from your pages with these commands:

```bash
co rem search "pilot"                    # find records by text
co rem show people/priya-natarajan.md    # read one page
co rem list people                       # browse a category
```

It is read-only. Finding a task in the notebook doesn't give the agent permission to do it.

### Skill pages: know which skills earn their place

co rem writes a page for every skill you have installed. Each page says:
- what the skill does;
- when you last used it;
- how its runs went, from the run records it finds.

When you have a hundred skills, this is how you find the five that matter.

### The investigation skills

The pages themselves are written by skills you can read and change:
- `rem-investigate-person`, `rem-investigate-project`, `rem-investigate-org` and `rem-investigate-skill` investigate one subject each;
- `rem-page-person`, `rem-page-project`, `rem-page-org` and `rem-page-skill` set what each page must contain;
- `rem-abstract` lifts settled decisions and recurring reasons out of the pages.

Investigations follow leads like a journalist: each round reads one part of the evidence, edits the page in place, and deletes what newer mail supersedes.

## Private by default

- The notebook is a folder on your machine: `~/.co/rem`.
- Saved mail bodies stay in its owner-only `.state/` folder and never appear on a page.
- A model reads them only through the login you choose (your Claude Code or Codex plan). It does not use OpenOnion credits.
- `co rem sources` shows what is read; `co rem sources remove <source>` stops it.

## Keep it current

```bash
co rem start            # approve sources and a daily schedule
co rem sync             # pull in the latest sessions now
co rem status           # coverage, last run, limits
```

## Learn more

- Guide: [docs.connectonion.com](https://docs.connectonion.com)
- Code: [openonion/connectonion](https://github.com/openonion/connectonion) (co rem lives in `connectonion/rem/`)
- Community: [Discord](https://discord.gg/4xfD9k8AUF)
