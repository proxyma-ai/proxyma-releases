# Proxyma desktop downloads

Official download host for the [Proxyma](https://proxyma.ai) desktop app.

**[Download the latest release](https://github.com/proxyma-ai/proxyma-releases/releases/latest)**

Every release page lists what changed in that version, alongside the files.

## Files

| Platform | File | Requirements |
|---|---|---|
| Windows | `proxyma-x64-v<version>.exe` | Windows 10 or 11, 64-bit |
| Linux | `proxyma-x64-v<version>.AppImage` | glibc distro, x86-64. `chmod +x`, then run |
| macOS | not built yet | - |

- Both builds are **self-contained** - the Java runtime and Python components ship inside them.
- `-update.zip` is for **Proxyma's own updater**, not for you. Downloading it by hand does nothing.
- `Source code (zip)` / `(tar.gz)` are attached by GitHub automatically and cannot be turned off.
  This repository holds no source, so they contain only this README.
- Releases before v1.1.0 also carry `proxyma-manual-*.zip` and `proxyma-release-notes-*.zip`.
  No longer produced - the manuals moved to [proxyma.ai/docs](https://proxyma.ai/docs/), so they
  are always current for the version you are running.

## Verify your download

Every asset carries a SHA-256 digest, shown next to the file on the release page.

```powershell
Get-FileHash .\proxyma-x64-v1.1.0.exe -Algorithm SHA256   # Windows
```

```bash
sha256sum proxyma-x64-v1.1.0.AppImage                     # Linux
```

**The Windows installer is not code-signed yet.** SmartScreen will warn that the publisher is
unrecognised - choose "More info", then "Run anyway". That is expected, and it is why checking the
digest above is worth the ten seconds. The [desktop manual](https://proxyma.ai/docs/desktop/) has
the exact wording and screenshots.

## Linking to a download

- `https://github.com/proxyma-ai/proxyma-releases/releases/latest` always resolves to the newest
  release. Safe to bookmark or link.
- There is **no fixed direct-download URL**: GitHub's `/releases/latest/download/<file>` shortcut
  needs an exact filename, and ours carry the version. Read the asset name from the API first:

```bash
curl -s https://api.github.com/repos/proxyma-ai/proxyma-releases/releases/latest \
  | grep -o '"browser_download_url": *"[^"]*\.AppImage"'
```

## Documentation and support

- [Release notes](https://proxyma.ai/docs/release-notes/) - the curated, cross-version account
- [Windows manual](https://proxyma.ai/docs/desktop/)
- [Linux manual](https://proxyma.ai/docs/linux/)
- [FAQ](https://proxyma.ai/docs/faq/)
- **contact@proxyma.ai**, or "Send feedback" inside the app

**Please do not open issues here.** This repository has no source and no issue tracker in use.

## About this repository

- Proxyma is **not open source**. This repo exists only because release downloads must be
  anonymous, which requires a public repository, while the product's own repo is private.
- It contains no source code and never will.
- Releases are published automatically when a `v*.*.*` tag is pushed in the private
  `proxyma-app` repo.

### Do not delete this README

A release needs a tag, a tag needs a commit, and **a repository with zero commits cannot have a
release created in it at all**. The API accepts the draft and every uploaded asset, then rejects
the *publish* with a bare `HTTP 422` when it tries to materialise the tag - after however long the
installer took to build, and naming neither the cause nor the repository.

This commit is what makes the repository publishable.
