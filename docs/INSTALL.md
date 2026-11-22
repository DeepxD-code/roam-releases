# Installing Roam

## Requirements
- Windows 10 or 11 (x64)
- [Git for Windows](https://git-scm.com/download/win)
- An **empty private git repo** to store your sessions (GitHub, GitLab, Gitea, your own server)
- At least one supported agent: OpenCode, Claude Code, Codex, Cursor, Gemini CLI, Antigravity, Crush or Aider

## 1. Create your private repo and clone it
On GitHub: **New repository → Private**. Then clone it to `roam-relay` in your home folder,
which is where Roam looks by default:
```powershell
git clone https://github.com/you/roam-relay.git $HOME\roam-relay
```
Roam pushes to it with your existing git credentials. (Somewhere else? Clone it there and
run `setx ROAM_RELAY_ROOT "<that folder>"`, then open a new terminal.)

## 2. Install
1. Download `roam-setup-x64-2.5.1.exe` from the [latest release](https://github.com/DeepxD-code/roam-releases/releases/latest).
2. Optional: check the file against the published SHA-256:
   ```powershell
   (Get-FileHash .\roam-setup-x64-2.5.1.exe -Algorithm SHA256).Hash.ToLower()
   ```
3. Run it. SmartScreen will say "Windows protected your PC" because the installer isn't
   code-signed yet: choose **More info → Run anyway**.
4. The setup wizard checks git is present, finds the agents on your machine, and asks which
   to capture.

Check everything is set up:
```powershell
roam auth check
```

## 3. Your second machine
Clone the **same** private repo to `$HOME\roam-relay` and install the same way. Then, in a project folder:
```powershell
roam resume
```
To let the two machines message each other (Pro), pair them:
`roam pair-request` on the new machine, `roam pair-approve --code XXXX-XXXX` on the old one.

## Everyday commands
| Command | What it does |
|---|---|
| `roam resume` | Latest session for this project, from any machine |
| `roam search <words>` | Search every captured session |
| `roam search --fresh <words>` | Pull from your repo first, then search |
| `roam inbox` | Messages from your other machines and agents |
| `roam ui` | Control page (turn capture on or off) |
| `roam --help` | Everything else |

Inside agents, the same things are tools: `roam_resume`, `roam_search`, `roam_inbox`, `roam_send`.

## First search after installing or updating
Roam builds a local search index once. On a very large history (several GB) this takes about
a minute and up to ~1.2 GB of RAM; after that, searches take seconds.

## Uninstall
`roam uninstall`, or **Settings → Apps → Roam → Uninstall**. Your private repo is not touched.
