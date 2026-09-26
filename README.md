<!--
  MAINTAINERS - please keep at least one commit in this repository.

  A GitHub release needs a tag, and a tag needs a commit. In a repository with zero commits a
  release cannot be created at all: the API accepts the draft and every uploaded asset, then
  rejects the PUBLISH with a bare "HTTP 422: Validation Failed" when it tries to materialize the
  tag - after however long the installer took to build, and naming neither the cause nor the
  repository. This file is what keeps the repository publishable. Do not empty it.

  Releases are published from our main repository by its release scripts, run by hand. The
  long-lived `parts` prerelease ("Proxyma parts") holds the pieces the installers download on the
  first start - do not delete it or its files.
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
| **Linux** | `proxyma_<version>_amd64.deb` | Ubuntu, Debian or another Debian-based distribution, x86-64 |
| **macOS** | Not available yet | - |

- The installers are **small**. The first time Proxyma starts, it downloads the rest of itself
  and shows the progress. That needs an internet connection once; later starts do not.
- On Linux, install the package with `sudo apt install ./proxyma_<version>_amd64.deb`.
- You may also see `parts-windows-x64.txt`, `parts-linux-x64.txt` and a release called
  **Proxyma parts**. Proxyma uses those itself to install and update - you do not need to download
  them.
- GitHub attaches **Source code (zip/tar.gz)** to every release automatically. Proxyma is not open
  source, so those archives contain only this page.

## Installing on Windows

Proxyma's installer is not yet signed with a commercial certificate, so Windows SmartScreen will
warn that the publisher is unrecognized.

- Choose **More info**, then **Run anyway** to continue.
- If you would rather confirm the file first, verify its checksum below - every release lists a
  SHA-256 for each file.

The [Windows manual](https://proxyma.ai/docs/desktop/) shows exactly what this looks like.

## Verifying your download

Compare the digest shown next to the file on the release page with the file you downloaded:

```powershell
# Windows (PowerShell)
Get-FileHash .\proxyma-x64-v0.16.0.exe -Algorithm SHA256
```

```bash
# Linux
sha256sum proxyma_0.16.0_amd64.deb
```

If the two values match, the download is intact.

## Linking to a download

- **`https://github.com/proxyma-ai/proxyma-releases/releases/latest`** always points at the newest
  version. It is safe to bookmark or share.
- There is no permanent direct-download link, because our filenames include the version number.
  To fetch the latest automatically, read the file name from the API first:

```bash
curl -s https://api.github.com/repos/proxyma-ai/proxyma-releases/releases/latest \
  | grep -o '"browser_download_url": *"[^"]*\.deb"'
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
