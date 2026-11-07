# fushi-linux — unofficial Linux builds of Fushi

Community Flatpak builds of [Fushi](https://github.com/hajisensai/Fushi) for Linux
desktops and the Steam Deck. This repo only holds release files and this page.

> **Unofficial.** These builds are not made or supported by the Fushi maintainers.
> Upstream does not publish Linux builds. Please report Linux-build problems here,
> not in the upstream repo.
>
> 非官方构建：Fushi 上游不发布 Linux 包，这里的 Flatpak 由社区自行构建。Linux 包的问题请在本仓反馈，不要开到上游。

## Install

Download `fushi-<version>-<commit>-x86_64.flatpak` from [Releases](../../releases), then:

```bash
flatpak install --user fushi-<version>-<commit>-x86_64.flatpak
flatpak run app.fushi.reader
```

The first install downloads the GNOME 49 runtime from Flathub (needs internet).
Fushi then appears in your app menu. On a Steam Deck, add it to Steam as a
non-Steam game to use it in Game Mode.

**To update:** download the newer release and run the same `flatpak install`
command. Your library and settings are kept (`~/.var/app/app.fushi.reader`).

**To remove:** `flatpak uninstall --user app.fushi.reader`
(add `--delete-data` to remove your data too).

## Limits

- x86_64 only (no ARM).
- No automatic updates and no signing: install files only from this repo's Releases.
- Features that need the official app's private keys (for example Google sign-in
  and log upload) may not work.
- Some features are Windows / macOS only upstream, for example Galgame Hook, the
  floating lyric window and in-app updates.

## Permissions

The app needs wide access to work as a reader and media player:

| Permission | Why |
|---|---|
| network, ipc | Online sources, dictionaries, Fushi Connect |
| X11 (pinned) + Wayland | The floating ball and overlays place their own windows, which Wayland does not allow; Wayland is used only to read the selected text |
| PulseAudio | Audio and video playback |
| all devices | GPU video decoding, gamepads |
| home, `/run/media` | Open your books, videos and music, including SD cards and USB drives |
| Secret Service, notifications, screensaver, tray, Avahi | Stored passwords, notifications, keep the screen on during playback, tray icon, LAN device discovery |

## Source

Fushi is GPL-3.0. Each release names the exact upstream commit it was built from.
The full source, including the Flatpak recipe
([`tool/linux/flatpak/`](https://github.com/hajisensai/Fushi/tree/develop/tool/linux/flatpak)),
is in [hajisensai/Fushi](https://github.com/hajisensai/Fushi) at that commit. The
recipe lists the exact source URLs and versions of the bundled third-party parts
(WebKit, mpv, ffmpeg and others).

To build the same file yourself (Docker; works from Linux or Git Bash on Windows):

```bash
git clone https://github.com/hajisensai/Fushi && cd Fushi
git checkout <commit>
bash tool/linux/build_in_docker.sh
bash tool/linux/flatpak/build_flatpak.sh
# -> build/linux-dist/fushi-<version>.flatpak
```

The first build compiles WebKit and takes several hours; later builds reuse the cache.

## License

GPL-3.0, see [LICENSE](LICENSE), same as upstream.
