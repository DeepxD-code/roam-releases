# macOS and Linux (preview)

**Status, honestly:** these builds are a preview. On every release they're built and tested on
real macOS (Apple Silicon) and Ubuntu machines in CI: capture, push to your git repo, search,
resume, the Free licence check, and start-at-login on/off all pass. The guided setup
(`roam install`) has code for macOS and Linux but hasn't been run on a real Mac or Linux desktop
yet. If something breaks, [open an issue](https://github.com/DeepxD-code/roam-releases/issues/new/choose)
and I'll fix it fast.

Builds: **macOS Apple Silicon (arm64)** and **Linux x64**. No Intel Mac or Linux arm64 build yet.

## 1. Download and check

From the [latest release](https://github.com/DeepxD-code/roam-releases/releases/latest), download
`roam-<version>-macos-arm64.tar.gz` or `roam-<version>-linux-x64.tar.gz`, plus `SHA256SUMS.txt`.

```bash
shasum -a 256 -c SHA256SUMS.txt --ignore-missing   # macOS
sha256sum -c SHA256SUMS.txt --ignore-missing       # Linux
```

## 2. Unpack and put `roam` on your PATH

Keep the three files together (`roam`, `roam-watch`, `roam-watch-bg`): Roam looks for its
scanner next to itself.

```bash
mkdir -p ~/.local/share/roam ~/.local/bin
tar -xzf roam-*-*.tar.gz -C ~/.local/share/roam --strip-components=1
ln -sf ~/.local/share/roam/roam ~/.local/bin/roam
roam --version
```

**macOS only:** the binaries are ad-hoc signed but not notarized (that needs a paid Apple
developer account), so Gatekeeper blocks them on first run. After checking the checksum:

```bash
xattr -dr com.apple.quarantine ~/.local/share/roam
```

## 3. Your private session repo

Create an **empty private** repo (GitHub, GitLab or your own server) and clone it:

```bash
git clone git@github.com:<you>/<your-relay>.git ~/roam-relay
```

## 4. Set up

```bash
roam install        # finds your agents and installs the OpenCode plugin / agent tools (preview)
roam startup on     # start capturing at login (launchd on macOS, systemd user unit on Linux)
roam auth check     # checks this machine is set up right
```

Then work as usual. `roam resume`, `roam search <words>` and the in-agent tools work the same
as on Windows; see [INSTALL.md](INSTALL.md) for the everyday commands.

## Remove

```bash
roam startup off
roam uninstall
rm -rf ~/.local/share/roam ~/.local/bin/roam
```

Your session repo is never touched by uninstall.
