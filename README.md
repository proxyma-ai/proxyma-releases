<!--
  MAINTAINERS - please keep at least one commit in this repository.

  A GitHub release needs a tag, and a tag needs a commit. In a repository with zero commits a
  release cannot be created at all: the API accepts the draft and every uploaded asset, then
  rejects the PUBLISH with a bare "HTTP 422: Validation Failed" when it tries to materialise the
  tag - after however long the installer took to build, and naming neither the cause nor the
  repository. This file is what keeps the repository publishable. Do not empty it.

  Releases are published automatically from our main repository when a v*.*.* tag is pushed.
-->

# Proxyma downloads

Official download host for the **[Proxyma](https://proxyma.ai)** desktop app - semantic search
and an AI agent over your own documents, running entirely on your machine.

### **[Download the latest version](https://github.com/proxyma-ai/proxyma-releases/releases/latest)**

Each release page lists what changed in that version, along with the files below.

## Which file do I need?

| Your system | Download | Requirements |
|---|---|---|
| **Windows** | `proxyma-x64-v<version>.exe` | Windows 10 or 11, 64-bit |
| **Linux** | `proxyma-x64-v<version>.AppImage` | Any glibc distribution, x86-64 |
| **macOS** | Not available yet | - |

- Both downloads are **self-contained**. Everything Proxyma needs is inside, so there is nothing
  to install beforehand.
- On Linux, mark the file executable before running it: `chmod +x proxyma-x64-*.AppImage`
- You may also see a `-update.zip` file. That one is used by Proxyma's built-in updater to update
  an existing installation - you do not need to download it yourself.
- GitHub attaches **Source code (zip/tar.gz)** to every release automatically. Proxyma is not open
  source, so those archives contain only this page.

## Installing on Windows

Proxyma's installer is not yet signed with a commercial certificate, so Windows SmartScreen will
warn that the publisher is unrecognised.

- Choose **More info**, then **Run anyway** to continue.
- If you would rather confirm the file first, verify its checksum below - every release lists a
  SHA-256 for each file.

The [Windows manual](https://proxyma.ai/docs/desktop/) shows exactly what this looks like.

## Verifying your download

Compare the digest shown next to the file on the release page with the file you downloaded:

```powershell
# Windows (PowerShell)
Get-FileHash .\proxyma-x64-v1.1.0.exe -Algorithm SHA256
```

```bash
# Linux
sha256sum proxyma-x64-v1.1.0.AppImage
```

If the two values match, the download is intact.

## Linking to a download

- **`https://github.com/proxyma-ai/proxyma-releases/releases/latest`** always points at the newest
  version. It is safe to bookmark or share.
- There is no permanent direct-download link, because our filenames include the version number.
  To fetch the latest automatically, read the file name from the API first:

```bash
curl -s https://api.github.com/repos/proxyma-ai/proxyma-releases/releases/latest \
  | grep -o '"browser_download_url": *"[^"]*\.AppImage"'
```

## Documentation

- **[Getting started and full manual](https://proxyma.ai/docs/desktop/)** - Windows
- **[Linux manual](https://proxyma.ai/docs/linux/)**
- **[Release notes](https://proxyma.ai/docs/release-notes/)** - what changed across versions
- **[Frequently asked questions](https://proxyma.ai/docs/faq/)**

## Help and feedback

- Email **contact@proxyma.ai**
- Or use **Send feedback** inside the app, which reaches us directly and can include diagnostics

This repository hosts downloads only and has no issue tracker, so please use one of the two
channels above - they are read by the people who build Proxyma.

## About this repository

Proxyma is a commercial product and is not open source. This repository exists so that downloads
are available to everyone without a GitHub account or sign-in; it contains no source code.

License terms are in the [End User License Agreement](https://proxyma.ai/eula), and
[pricing is here](https://proxyma.ai/pricing).
