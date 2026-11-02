# APT Repository for Obsidian & Chirpity

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A simple APT repository for installing and updating [Obsidian](https://obsidian.md/) and [Chirpity](https://chirpity.net/).

## Supported Applications

| Application | Upstream format | APT package |
|---|---|---|
| [Obsidian](https://obsidian.md/) | `.deb` | `obsidian` |
| [Chirpity](https://chirpity.net/) | AppImage | `chirpity` |

Chirpity's AppImage is automatically packaged as a `.deb`, including desktop integration.

## Important: Repository Signing Configuration

Before this project can work correctly, the repository signing keys must be configured.

### 1. Configure the signing key pair

In `conf/distributions`, configure the `SignWith` option with a custom public/private key pair.

These keys are used to sign the APT repository, allowing clients to verify the authenticity and integrity of the published packages.

### 2. Configure GitHub Actions

Add a repository secret named `APT_SIGNING_KEY` to your GitHub repository.

The secret must contain the **private signing key** corresponding to the public key configured above.

GitHub Actions uses this secret to sign the repository during the publishing process.

**Important:** Never commit your private signing key to the repository or expose it in logs or other public places.

## Add the Repository

Import the repository's public signing key and configure APT:

```bash
sudo install -d -m 0755 /etc/apt/keyrings

curl -fsSL https://tialu06.github.io/github-apt-repo/apt-repo-public-key.asc \
  | sudo gpg --dearmor --yes -o /etc/apt/keyrings/github-apt-repo.gpg

sudo chmod 0644 /etc/apt/keyrings/github-apt-repo.gpg

echo "deb [signed-by=/etc/apt/keyrings/github-apt-repo.gpg arch=amd64] https://tialu06.github.io/github-apt-repo stable main" \
  | sudo tee /etc/apt/sources.list.d/github-apt-repo.list

sudo apt update
```

Install either application:
```bash
sudo apt install obsidian
sudo apt install chirpity
```

Update installed applications normally:
```bash
sudo apt update
sudo apt upgrade
```

## Automation

GitHub Actions checks upstream releases daily. When an application changes, the workflow downloads and packages the new version, updates the APT repository, and publishes it. Unchanged application packages are reused.

A separate monthly keep-alive workflow creates a nearly empty commit to help prevent GitHub Actions scheduled workflows from being disabled due to repository inactivity. This is a workaround, not a guarantee that scheduled workflows will remain enabled.
## License

The repository's code, workflows, and packaging configuration are licensed under the MIT License. Obsidian and Chirpity remain subject to their respective licenses. This repository is not affiliated with or endorsed by either project.
