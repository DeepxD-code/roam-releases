# Privacy: what Roam reads, writes and sends

Roam reads your agents' session transcripts. That's a lot of trust, so here is exactly what
happens to them.

## What Roam reads
- Session files of the agents you choose during setup (for example OpenCode's sessions,
  Claude Code's `~/.claude/projects`, Codex and Cursor transcripts).
- Basic git information about the project you're working in (branch, changed files).

## What Roam writes, and where
- A markdown handoff per session, committed to **the private git remote you configure**.
- Local state and a search index on your own machine.
- **Secrets are scrubbed before anything is written:** API keys and tokens (Stripe, npm,
  Hugging Face, GitLab, SendGrid, Telegram, Discord and Slack webhooks, and more),
  credentials in URLs, secret-looking JSON fields and command-line flags, and PowerShell
  `$env:` / `setx` lines. The test suite covers 29 patterns. Scrubbing is a safety net,
  not a guarantee: don't paste secrets into agents.

## What Roam sends over the network
| Request | When |
|---|---|
| `git push` / `git pull` to **your** remote | Whenever sessions sync |
| One small version file from the Roam website | Only when you run `roam update` |
| Rust toolchain download from rustup.rs (checksum-verified) | Only during install, only if it's missing |
| Telegram / Discord / Tailscale | Only if you set up those optional Labs features |

**No telemetry. No analytics in the app. No Roam account. No Roam server.**
The Roam website itself uses cookieless page counts (Vercel Web Analytics); the app doesn't.

## Optional encryption
You can turn on shared-key encryption between your paired machines (AES-256-GCM, with keys
exchanged using each device's key pair). Without it, your sessions are protected by your
private repo's access control, the same as your code.

## Deleting data
`roam forget <session>` removes a session; deleting your private repo removes everything.
`roam uninstall` removes Roam from your machine and leaves your repo alone.
