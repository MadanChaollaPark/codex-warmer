# codex-warmer

A small cron-friendly wrapper that pings `codex exec` on a schedule so the
Codex 5-hour usage window stays open and overlaps the next one — giving you a
"warmer" of usable quota right when you sit down to work.

## Install

```bash
mkdir -p ~/bin ~/logs
install -m 755 codex-warmer ~/bin/codex-warmer
```

The wrapper assumes Codex is installed via `nvm` and that you've authenticated
with `codex login` using your ChatGPT account. API-key auth has no rolling
5-hour window, so the warmer would do nothing for you in that mode.

## Schedule

Add this line via `crontab -e`:

```cron
0 */4 * * * $HOME/bin/codex-warmer >> $HOME/logs/codex-warmer.log 2>&1
```

That fires at 00:00, 04:00, 08:00, 12:00, 16:00, 20:00 — so each new 5-hour
window opens roughly an hour before the previous one closes, leaving you with
overlapping quota whenever you start a session.
