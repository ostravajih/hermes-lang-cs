# hermes-lang-cs — Czech (Čeština) language pack for Hermes Agent

Czech interface strings for **Hermes Agent**: the core (CLI approval prompts, gateway replies,
tool verbs, tips), the Ink TUI (`hermes --tui`) and the Hermes Desktop app — from one pack.

Text-only: no code that runs, no network access, no permissions, no dependencies. Just catalogs.

## Install

```bash
hermes plugins install ostravajih/hermes-lang-cs   # or: hermes plugins install <catalog name>
hermes config set display.language cs
```

Restart any running gateway or TUI so the pack is picked up. In the Desktop app the language
appears in the language switcher as **Čeština**; `HERMES_LANGUAGE=cs` in `.env` still wins over
`display.language`.

Without the pack, a personal overlay also works: drop `locales/cs.yaml` (and optionally
`cs.tui.yaml` / `cs.desktop.yaml`) into `~/.hermes/locales/`.

## What is covered

| Surface | File | Keys |
| --- | --- | --- |
| Core (CLI, gateway, approvals, tips) | `locales/cs.yaml` | 3510 |
| Ink TUI | `locales/cs.tui.yaml` | 1386 |
| Hermes Desktop | `locales/cs.desktop.yaml` | 5360 |

Key sets are kept equal to the English catalogs of Hermes Agent `ef75bc70` (2026-10-29), verified by
flattening both sides and diffing the key sets, including function-backed entries.

### Known fallbacks

Entries whose English value is a *function with branching* (plural counts such as `cron.count`,
`sidebar.messageCount`, or labels that swap on a condition such as
`assistant.thread.errorSwitchToModel`) cannot be expressed as a single template in the pack format.
Those 125 Desktop keys (plus two array values) are left out on purpose and render in English rather than in a wrong Czech
form ("1 zpráv"). The core and TUI catalogs have no such gaps: positional `{0}` templates cover
every function-backed entry there.

`settings.sessions.defaultDirUpdated` is a special case: its English value takes an optional keyboard
shortcut and wraps it in brackets only when present, which a pack template cannot do, so the Czech
text names the action without the shortcut.

Two strings in `locales/cs.yaml` (`display.verb_connector.search` / `.default`) drop an invisible
zero-width space that the upstream English catalog keeps for spacing; the install scanner flags it
as a HIGH-severity finding, and the visible result is identical without it.

## Where the translations come from

Hand-reviewed Czech catalogs maintained at
[ostravajih/hermes-agent `feat/i18n-czech`](https://github.com/ostravajih/hermes-agent/tree/feat/i18n-czech)
(upstream PR [NousResearch/hermes-agent#105503](https://github.com/NousResearch/hermes-agent/pull/105503)),
synced against `upstream/main` (`ef75bc70`) on 2026-10-29. This pack ships the same text so Czech users are not
blocked while that PR waits for review; if the PR lands, the bundled locale and this pack agree.

## License

MIT — see [LICENSE](LICENSE).
