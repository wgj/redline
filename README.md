# usage-pacing

Live rate-limit checkers for **Claude.ai** (Max/Pro) and **OpenAI** (Plus/Pro/Codex) with automatic pacing tiers for AI agents.

Built for [OpenClaw](https://github.com/openclaw/openclaw) but the scripts work standalone too.

## What it does

- **`claude-usage`** — Checks your Claude.ai plan usage (5-hour window, weekly, extra credits) via the Anthropic OAuth API
- **`openai-usage`** — Checks your OpenAI/Codex plan usage (primary/secondary rate windows, credits) via the ChatGPT API
- **Pacing tiers** — GREEN/YELLOW/ORANGE/RED system to automatically throttle agent behavior as limits approach

## Quick start

```bash
# Claude usage (requires `claude login` for OAuth token)
./scripts/claude-usage

# OpenAI usage (requires OpenClaw auth or manual token setup)
./scripts/openai-usage

# JSON output for programmatic use
./scripts/claude-usage --json
./scripts/openai-usage --json
```

## Sample output

```
  Claude Usage (default_claude_max_5x)
  ────────────────────────────────────────
    5-Hour  ████████░░░░░░░░░░░░ 61% left  resets 09:00 PM Feb 17
    Weekly  ██░░░░░░░░░░░░░░░░░░ 88% left  resets 08:00 PM Feb 23
   Credits  ████████████████████ 0% left  $5044/5000 used

  OpenAI Usage  plan: plus
    5h  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ 100% left  resets 10:50 PM MST
   Day  ██████████░░░░░░░░░░░░░░░░░░░░ 66% left  resets 9:15 AM MST
  Credits: $882.99
```

## Pacing tiers

| Tier | Remaining | Agent behavior |
|------|-----------|----------------|
| 🟢 GREEN | >50% | Normal operations |
| 🟡 YELLOW | 25–50% | Skip sub-agents, defer non-urgent work |
| 🟠 ORANGE | 10–25% | Essential replies only |
| 🔴 RED | <10% | Critical only, warn user |

## Requirements

- Python 3.8+
- **Claude checker:** macOS Keychain with Claude Code OAuth token (`claude login`)
- **OpenAI checker:** OpenClaw auth-profiles with `openai-codex` profile, OR manual token

## As an OpenClaw skill

```bash
clawhub install usage-pacing
```

Then add the pacing logic to your `HEARTBEAT.md` — see [SKILL.md](SKILL.md) for details.

## License

MIT
