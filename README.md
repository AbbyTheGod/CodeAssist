# CodeAssist Installation Guide (WSL 2 & Linux)

Installation guide for CodeAssist. All commands below work for both WSL 2 and Linux.

> **What is WSL 2?** WSL 2 (Windows Subsystem for Linux) is a feature in Windows that lets you run a Linux environment directly on Windows. If you're on Windows, you can use WSL 2 instead of dual-booting or using a VM.

## System Requirements

- **RAM**: 12 GB minimum (32 GB recommended)
- **Storage**: 10 GB free space
- **OS**: Windows with WSL 2, or Linux (Ubuntu 22.04+)

## Prerequisites

### 1. Docker

```bash
sudo apt update -y && sudo apt upgrade -y

for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update

sudo apt-get install ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo docker run hello-world

sudo service docker start

sudo usermod -aG docker $USER
```

> **Note**: After adding yourself to the docker group, exit and restart your terminal/WSL session for changes to take effect.

### 2. Python 3.10+

```bash
python3 --version
```

If not installed:
```bash
sudo apt install python3.10
```

### 3. UV

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 4. Git

```bash
sudo apt install git
```

### 5. HuggingFace Token

1. Go to [HuggingFace](https://huggingface.co/settings/tokens)
2. Create a token with `Write` access
3. Save it for later use

## Installation

```bash
git clone https://github.com/gensyn-ai/codeassist.git
cd codeassist
uv run run.py
```

Enter your HuggingFace token when prompted.

Access the web UI at `http://localhost:3000` and log in (Gensyn Testnet account is auto-created).

## Troubleshooting

**Docker not running:**
```bash
sudo service docker start
```

**Permission denied:**
```bash
sudo usermod -aG docker $USER
```

**Port 3000 in use:**
Stop the conflicting service or change the port.

## Resources

- [Official Docs](https://docs.gensyn.ai/testnet/codeassist/getting-started)
- [GitHub Repository](https://github.com/gensyn-ai/codeassist)
