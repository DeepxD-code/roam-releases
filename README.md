# Roam

**Let your coding agents share memory and message each other — across machines, across agents.**

Roam saves every OpenCode, Claude Code, Codex, Cursor and Gemini CLI session to a private
git repo **you** choose. On your other machine, or in a different agent, you pick up exactly
where you stopped: `roam resume` brings back the latest session, `roam search` finds
anything older, and agents can leave each other signed notes.

No Roam server. No account. Your sessions only ever go to your own repo.

**[Download for Windows (v2.5.1)](https://github.com/DeepxD-code/roam-releases/releases/latest)** ·
[Website](https://roam-rho-gold.vercel.app) · [Install guide](docs/INSTALL.md) ·
[Privacy](docs/PRIVACY.md) · [FAQ](docs/FAQ.md) · [Changelog](CHANGELOG.md)

---

## What it does

| | |
|---|---|
| **Capture** | Each agent session becomes a markdown handoff: prompts, answers, files touched, todos. OpenCode through a live plugin; Claude Code, Codex, Cursor, Gemini CLI, Antigravity, Crush and Aider through a small background watcher. |
| **Sync** | Handoffs are committed to a private git remote you own (GitHub, GitLab, your own server). Append-only: git stores each new line once. |
| **Resume** | `roam resume` (or `roam_resume` inside the agent) loads the latest session for this project, from any machine. |
| **Search** | `roam search <words>` searches every session, on every machine, in every agent. A local index keeps it fast. |
| **Agents talk to each other** | `roam_send` / `roam_inbox`: an agent on one machine can leave a signed note for the agents on another, or for a different agent on the same machine. |
| **MCP server** | `roam serve` exposes `roam_search`, `roam_resume`, `roam_inbox` and more to any MCP-capable agent. |
| **Secret scrubbing** | API keys, tokens, connection strings and similar are removed before anything is written. |

## Measured, not promised

On a real 4.8 GB session history (Windows laptop, November 2026):

| | |
|---|---|
| `roam search`, rare word | ~0.6 s |
| `roam search`, very common word | ~5 s |
| `roam_search` inside OpenCode | 1–3 s rare word, ~8 s common word |
| First index build (one-time) | 78 s, 1.2 GB RAM |
| Same-machine message delivery | a local file write (5–37 ms) |
| Two-machine test (separate Windows VM) | 7/7 checks pass: each machine finds and resumes the other's sessions |

## Quick start

1. Make a **private repo** on GitHub (or anywhere git can push) and clone it:
   `git clone <your-private-repo-url> $HOME\roam-relay`
2. Download `roam-setup-x64-2.5.1.exe` from [Releases](https://github.com/DeepxD-code/roam-releases/releases/latest) and run it.
   Windows SmartScreen will warn once: the installer isn't code-signed yet. Verify it with the published SHA-256 if you like.
3. The setup finds your agents and asks which to capture.
4. Work as usual. On your other machine: clone the same repo to `$HOME\roam-relay`, install, run `roam resume`.

Full guide: [docs/INSTALL.md](docs/INSTALL.md).

## Agent skill

[`skills/roam/SKILL.md`](skills/roam/SKILL.md) is a free skill that tells your agent when to use
Roam: `roam_resume` at the start of a session, `roam_search` before asking you about past work,
and `roam_send` / `roam_inbox` to hand work between agents. Drop the `roam` folder into your
agent's skills folder (for Claude Code: `~/.claude/skills/`). It needs Roam installed.

## Platforms

- **Windows 10/11:** supported.
- **macOS (Apple Silicon) / Linux x64:** preview builds on every release, tested in CI on real macOS and Ubuntu machines. See [docs/INSTALL-MAC-LINUX.md](docs/INSTALL-MAC-LINUX.md). The guided setup hasn't been run on a real Mac or Linux desktop yet, so [tell me](https://github.com/DeepxD-code/roam-releases/issues/new/choose) if anything breaks.

## Free and Pro

| | Free | Pro (₹1,499 / 6 months) |
|---|---|---|
| Capture, resume and search on your machine | ✅ | ✅ |
| All supported agents, MCP server, secret scrubbing | ✅ | ✅ |
| Pair machines and message between them | | ✅ |
| Semantic search, voice notes, PR summaries, stats (Labs) | | ✅ |

## Bugs and ideas

Please [open an issue](https://github.com/DeepxD-code/roam-releases/issues/new/choose).
Run `roam feedback` to write a diagnostic report you can attach (it's written locally; nothing is sent).

## License

Roam is proprietary software by DeepxD-code. The Free tier is free to download and use;
the source code isn't public. This repository holds documentation and release builds.

Security reports: see [SECURITY.md](SECURITY.md).
