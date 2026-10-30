<!--
  MAINTAINERS - please keep at least one commit in this repository.

  A GitHub release needs a tag, and a tag needs a commit. In a repository with zero commits a
  release cannot be created at all: the API accepts the draft and every uploaded asset, then
  rejects the PUBLISH with a bare "HTTP 422: Validation Failed" when it tries to materialise the
  tag - after however long the installer took to build, and naming neither the cause nor the
  repository. This file is what keeps the repository publishable. Do not empty it.

  Releases are published from the main repository by tools/release/publish.sh, run by hand.
-->

# Proxyma downloads

Official download host for **[Proxyma](https://proxyma.ai)** - an AI assistant for your own
documents: hybrid search and an agent over your folders, wikis, tickets, repositories and mail,
with cited answers. It runs on your machine.

### **[Download the latest version](https://github.com/proxyma-ai/proxyma-releases/releases/latest)**

Each release page lists what changed in that version, along with the files below.

## Which file do I need?

| You want | Download | Needs |
|---|---|---|
| **Desktop on Windows** | `proxyma-x64-v<version>.exe` | Windows 10 or 11, 64-bit |
| **Desktop on Ubuntu or Debian** | `proxyma_<version>_amd64.deb`, or the APT repository below | x86-64, a desktop session |
| **Home Server** (one person, in Docker) | `proxyma-homeserver-<version>-compose.tar.gz` | Docker |
| **Enterprise Server** (a team, in Docker) | `proxyma-enterprise-server-<version>-compose.tar.gz` | Docker |
| **Kubernetes** | `proxyma-community-<version>.tgz` or `proxyma-enterprise-<version>.tgz` (Helm charts) | Kubernetes 1.27 or newer |
| **macOS** | Not available yet | - |

- The Desktop installers are small. The first start downloads the rest of Proxyma, about 650 MB,
  and later updates download only what changed.
- `parts-*.txt` and `SHA256SUMS*` are what the built-in updater and you use to check a download.
  You do not need to open them otherwise.
- Releases marked **Pre-release** are development builds for testing. Installations are offered
  them only with **Settings > Updates > Development builds** turned on.

## Ubuntu and Debian: the APT repository

```bash
sudo install -d -m 0755 /etc/apt/keyrings
sudo wget -qO /etc/apt/keyrings/proxyma.asc https://proxyma.ai/keys/proxyma-release.asc
echo "deb [signed-by=/etc/apt/keyrings/proxyma.asc] https://github.com/proxyma-ai/proxyma-releases/releases/download/apt/ ./" | sudo tee /etc/apt/sources.list.d/proxyma.list
sudo apt update && sudo apt install proxyma
```

The key's fingerprint is `BE3A B092 AB25 4FA4 5C57  8AF4 F571 F889 94F6 B817`.

## Windows: the SmartScreen warning

The installer is not signed with a commercial code-signing certificate, so SmartScreen may say the
publisher is unrecognized. Check the file came from this page, then choose **More info**, then
**Run anyway**.

## Verifying a download

Every release carries `SHA256SUMS.txt`, signed with the release key above (`SHA256SUMS.txt.asc`):

```bash
gpg --import proxyma-release.asc            # from https://proxyma.ai/keys/proxyma-release.asc
gpg --verify SHA256SUMS.txt.asc SHA256SUMS.txt
sha256sum --check --ignore-missing SHA256SUMS.txt
```

On Windows, compare `Get-FileHash .\proxyma-x64-v<version>.exe -Algorithm SHA256` with the line for
that file in `SHA256SUMS.txt`. The Docker images are signed with cosign:

```bash
cosign verify --key https://proxyma.ai/keys/cosign-release.pub ghcr.io/proxyma-ai/proxyma-homeserver:<version>
```

## Linking to a download

`https://github.com/proxyma-ai/proxyma-releases/releases/latest` always points at the newest
version. File names include the version, so there is no permanent direct link to a file.

## Documentation and help

- **[Manual](https://proxyma.ai/docs/manual/)** - installing, every edition, sources, the agent
- **[Release notes](https://proxyma.ai/docs/release-notes/)**
- Email **contact@proxyma.ai**, or **Send feedback** inside the app

This repository hosts downloads only and has no issue tracker.

## Source code

**Proxyma Community** is free software under the GNU AGPL v3; its source is at
**[proxyma-ai/proxyma-community](https://github.com/proxyma-ai/proxyma-community)**. Proxyma
Enterprise and the add-ons are commercial - see [pricing](https://proxyma.ai/pricing) and the
[End User License Agreement](https://proxyma.ai/eula). The "Source code" archives GitHub attaches to
every release contain only this page.
