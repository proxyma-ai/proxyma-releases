# Proxyma releases

Download host for [Proxyma](https://proxyma.ai) desktop builds. Every release here is published
automatically by `release-desktop.yml` in the private `proxyma-app` repository when a `v*.*.*`
tag is pushed there.

Each release carries:

| File | What it is |
|---|---|
| `proxyma-x64-v<version>.exe` | Windows installer - this is the one to download |
| `proxyma-x64-v<version>-update.zip` | Update payload, fetched by the app's own updater |
| `proxyma-manual-v<version>.zip` | User manual as HTML. Unzip and open `index.html` |
| `proxyma-release-notes-v<version>.zip` | Release notes as HTML, same idea |

Both HTML bundles are self-contained and work with no internet connection.

**This repository holds no source code.** It exists only because GitHub releases have to live in
a public repository for anonymous downloads to work, and `proxyma-app` is private.

## Why this file exists

A release needs a tag, and a tag needs a commit. A repository with zero commits cannot have a
release created in it at all: the API accepts the draft and its assets, then rejects the publish
with `HTTP 422` when it tries to materialize the tag. This commit is what makes the repository
publishable. Do not delete it to "clean up".
