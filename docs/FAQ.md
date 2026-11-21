# FAQ

**Claude Code / Codex already resume sessions. Why Roam?**
They resume on the same machine, in the same agent. Roam is for the other machine and the other agent: start in OpenCode on your desktop, continue in Claude Code on your laptop.

**Why git, not a database or a cloud?**
So there's no Roam server holding your sessions. You already trust your git host with your code; Roam keeps your sessions next to it, in a private repo you control.

**Can agents really talk to each other?**
Yes. Each agent gets `roam_send` / `roam_inbox` (plugin tools in OpenCode, MCP tools elsewhere). A message is a short note signed with the sending machine's key; the other agent pulls only what it needs with `roam_search` instead of receiving a whole transcript. On one machine delivery is a local file write; across machines it arrives on the next git sync. An agent sees new mail when it checks its inbox; it isn't pushed into a running session.

**Is my data sent anywhere?**
Only to the git remote you configure. No telemetry, no account, no Roam server. See [PRIVACY.md](PRIVACY.md) for every network request Roam can make.

**Is it encrypted?**
Optionally, between paired machines. Otherwise your private repo's access control protects it, the same as your code.

**Is it open source?**
Not at the moment. This repo has documentation and release builds; issues are welcome.

**Mac / Linux?**
Builds pass CI on macOS and Ubuntu, but installers aren't published yet. Open an issue if you'd use one.

**Windows flagged the installer.**
It isn't code-signed yet. The SHA-256 is published with every release so you can verify the file.

**How fast is search?**
On a 4.8 GB history: about 0.6 s for a rare word, about 5 s for a very common one. The first search after installing builds an index once (about a minute and up to 1.2 GB of RAM on a history that size).

**What does Pro cost and include?**
₹1,499 for 6 months (about US$18): pairing machines and messaging between them, semantic search, and the Labs extras (voice notes, PR summaries, stats, phone intake). Capture, resume and search on your machine are free.

**How do I pay from outside India?**
Email official.supercube@gmail.com for now; card checkout is coming.
