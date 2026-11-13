# REM privacy notice

Updated 13 November 2026.

REM is published by ConnectOnion. This notice covers the REM plugin and the
local notebook workflows it invokes through the ConnectOnion CLI.

## Information used

REM can process the sources you authorize, including connected Gmail or Outlook
mail, contacts and message metadata, and local Codex or Claude Code sessions.
These sources can contain names, contact details, correspondence, project
information, decisions, and details about other people. Additional sources
depend on your CLI configuration. The notebook records derived pages, source
references, cached source material, and run information.

REM uses this information to build and update your notebook, retrieve relevant
context, and answer your questions with sources. Source access and scheduled
work depend on your installed CLI version and configuration. The plugin explains
the setup effects before running initialization. Installing the plugin adds
its instructions. Starting setup can read sources, make model calls, and enable
background work.

## Storage and recipients

The notebook is stored on your computer, normally under `~/.co/rem`. Source
material may be cached locally so that pages can cite and revisit it. Your
coding agent also handles the requests and results you use in conversation.

Model processing sends selected source material and instructions to the service
used by your configured runner. This can be your Codex or Claude Code service,
or another model service configured in the CLI. Its account settings, privacy
terms, retention rules, and usage limits apply. Connected source providers
handle access to their services under their own policies. Package installation
and software updates contact the relevant package hosts.

Publishing the REM plugin does not give ConnectOnion access to your local
notebook. Other ConnectOnion services you choose to use have their own data
flows. A configured remote model service or an enabled notification channel
may receive content. Review your runner, sources, and notification settings
before approving setup. If automatic task execution is enabled, background
work can carry out configured tasks as well as update the notebook. Notification
content is sent to the recipients and channels configured for those workflows.

## Retention and controls

Notebook pages and cached source material remain on your machine until removed
by you or by the cleanup behavior of your installed CLI. REM has no single
fixed retention period across those local files. Source providers and model
services determine retention for the copies they process.

You can inspect source settings with `co rem sources`, configuration with
`co rem config`, and scheduled activity with `co rem status`.
`co rem stop` stops future scheduled updates. `co rem sources remove SOURCE`
removes a source from future reading. These actions can leave existing pages
and cached evidence in place. Current CLI setup may include newly connected
mailboxes automatically, so review the source settings when connecting accounts.

To remove your local notebook, stop upkeep and any running work before deleting
its configured folder. Copies in backups and conversations require separate
removal. Revoke mailbox access through your Google or Microsoft account when
you want to disconnect that service. Uninstalling the plugin removes its
instructions, and can leave the separately installed CLI and notebook in place.

## Support and changes

For privacy questions, use the publisher contact shown in the plugin directory
or the repository's support links. A public issue or community message is
visible to others, so include only information you want to share publicly.
We update this notice as the plugin's data practices change.
