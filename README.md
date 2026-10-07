# APT Repository for Obsidian & Chirpity

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A simple APT repository for installing and updating [Obsidian](https://obsidian.md/) and [Chirpity](https://chirpity.net/).

The repository is automatically checked for new releases every hour using GitHub Actions. When a new version is available, it is downloaded, packaged as a `.deb`, and added to the repository.

If no update is available, the workflow exits without downloading anything.

## Supported Applications

| Application | Source | Package |
|---|---|---|
| [Obsidian](https://obsidian.md/) | `.deb` | `obsidian` |
| [Chirpity](https://chirpity.net/) | AppImage | `chirpity` |

### Chirpity

Chirpity does not provide a `.deb` package upstream. This repository automatically wraps its AppImage in a `.deb` package, including desktop integration such as the application icon and menu entry.

This allows Chirpity to be installed and updated using the same APT workflow as a regular Debian package.

## How It Works

1. GitHub Actions checks for new upstream releases every hour.
2. The latest version is compared with the version already in the repository.
3. If there is no update, the workflow stops.
4. If a new version is available, the required files are downloaded and packaged.
5. The updated `.deb` is added to the APT repository.

This keeps the repository up to date without repeatedly downloading unchanged files.

## Using the Repository

> **Note:** This repository is primarily intended for personal use. If you want to use it yourself, you will need to replace the repository's GPG signing key with your own.

Once configured, the packages can be installed and updated using the standard APT commands:

```bash
sudo apt update
sudo apt install obsidian
sudo apt install chirpity
```

Future updates can be installed with:
```bash
sudo apt update
sudo apt upgrade
```

## License
The code, scripts, GitHub Actions workflows, and packaging configuration in this repository are licensed under the MIT License.

Obsidian and Chirpity are third-party software and remain subject to their respective licenses. This repository is not affiliated with or endorsed by either project.
