# Proxyma desktop downloads

Official download host for the [Proxyma](https://proxyma.ai) desktop app. Every build here is
published automatically when a `v*.*.*` tag is pushed in the private `proxyma-app` repository.

**[Download the latest release](https://github.com/proxyma-ai/proxyma-releases/releases/latest)**

## Download

| Platform | File | Requirements |
|---|---|---|
| Windows | `proxyma-x64-v<version>.exe` | Windows 10 or 11, 64-bit |
| Linux | `proxyma-x64-v<version>.AppImage` | glibc distribution, x86-64. `chmod +x` it, then run it |
| macOS | not built yet | - |

Both builds are self-contained: the Java runtime and the Python components ship inside them, so
there is nothing to install first.

This URL always resolves to the newest release, so it is safe to bookmark or link to:

```
https://github.com/proxyma-ai/proxyma-releases/releases/latest
```

Note that GitHub's `/releases/latest/download/<file>` shortcut needs the exact filename, and ours
carry the version - so there is no fixed direct-download link. To script a download, read the asset
name from the API first:

```bash
curl -s https://api.github.com/repos/proxyma-ai/proxyma-releases/releases/latest \
  | grep -o '"browser_download_url": *"[^"]*\.AppImage"'
```

## Verify your download

Every asset on a GitHub release carries a SHA-256 digest, shown next to the file on the release
page. Compare it against the file you downloaded:

```powershell
# Windows (PowerShell)
Get-FileHash .\proxyma-x64-v1.1.0.exe -Algorithm SHA256
```

```bash
# Linux
sha256sum proxyma-x64-v1.1.0.AppImage
```

**The Windows installer is not code-signed yet.** SmartScreen will warn that the publisher is
unrecognised, and you have to choose "More info" then "Run anyway" to proceed. That is expected
today and is the reason the checksum above is worth actually checking. See the
[desktop manual](https://proxyma.ai/docs/desktop/) for the exact wording and screenshots.

## What each file is

| File | Who it is for |
|---|---|
| `proxyma-x64-v<version>.exe` | **You.** The Windows installer |
| `proxyma-x64-v<version>.AppImage` | **You.** The Linux build, from v1.1.0 onward |
| `proxyma-x64-v<version>-update.zip` | **The app, not you.** Proxyma's own updater downloads this to update an existing Windows installation in place. Downloading it by hand does nothing useful |
| `Source code (zip)` / `(tar.gz)` | **Nobody.** GitHub attaches these to every release automatically and they cannot be turned off. This repository holds no source code, so they contain only this README |

Releases before v1.1.0 also carry `proxyma-manual-*.zip` and `proxyma-release-notes-*.zip`. Those
are no longer produced: the manuals and release notes are published on
[proxyma.ai/docs](https://proxyma.ai/docs/) instead, so they are the same for everyone and always
current for the release you are actually running.

## Documentation and support

| | |
|---|---|
| Release notes | https://proxyma.ai/docs/release-notes/ |
| Windows manual | https://proxyma.ai/docs/desktop/ |
| Linux manual | https://proxyma.ai/docs/linux/ |
| Questions and answers | https://proxyma.ai/docs/faq/ |
| Contact | contact@proxyma.ai |

**Please do not open issues here.** This repository has no source and no issue tracker in use -
mail contact@proxyma.ai instead, or use "Send feedback" inside the app, which reaches us directly.

## About this repository

Proxyma is not open source. This repository exists only because release downloads have to be
anonymous, which requires a public repository, and the product's own repository is private. It
contains no source code and never will.

### Why this README exists

A release needs a tag, and a tag needs a commit. A repository with zero commits cannot have a
release created in it at all: the API accepts the draft and every asset, then rejects the *publish*
with a bare `HTTP 422` when it tries to materialise the tag - after however long the installer took
to build. This commit is what makes the repository publishable.

**Do not delete it to "clean up".**
