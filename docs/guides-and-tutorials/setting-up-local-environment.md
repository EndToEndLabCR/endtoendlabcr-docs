---
sidebar_position: 2
---

# Setting Up Your Local Environment

This guide walks you through setting up a complete development environment for EndToEndLabCR projects. It takes about **1–2 hours** depending on your internet speed and whether you already have some of these tools installed.

> **You don't need everything.** Pick the tools that match the stack you plan to contribute to. A Python contributor doesn't need Java, and a frontend contributor doesn't need Maven.

Prefer detailed IDE guides? See [VS Code setup](../install-and-setup/installing-and-setting-up-vscode.md), [PyCharm setup](../install-and-setup/installing-and-setting-up-pycharm.md), and [Homebrew install](../install-and-setup/install-brew.md).

## Prerequisites

- Administrative access to your machine
- A stable internet connection
- A GitHub account

## Step 1: Install a Package Manager

### macOS — Homebrew

See our dedicated [Homebrew install guide](../install-and-setup/install-brew.md). Quick version:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

### Windows — Chocolatey

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

### Linux (Ubuntu/Debian)

```bash
sudo apt update && sudo apt upgrade -y
```

## Step 2: Install Core Tools

Install only what you need for the stacks you'll work with.

### Recommended Baseline (everyone)

| Tool   | macOS                        | Windows                | Linux                     |
| ------ | ---------------------------- | ---------------------- | ------------------------- |
| Git    | `brew install git`           | `choco install git`    | `sudo apt install -y git` |
| Node   | `brew install node`          | `choco install nodejs` | See NodeSource below      |
| Docker | `brew install --cask docker` | Docker Desktop         | See Docker section below  |

### Python Stack

```bash
# macOS
brew install python@3.11

# Windows
choco install python -y

# Linux
sudo apt install -y python3 python3-pip python3-venv
```

Use `venv` + `pip` for dependency management:

```bash
# Create and activate a virtual environment
python3 -m venv venv

# macOS/Linux
source venv/bin/activate

# Windows
venv\Scripts\activate

# Install project dependencies
pip install -r requirements.txt
```

### Java / Spring Boot Stack

```bash
# macOS
brew install java maven

# Windows
choco install java maven -y

# Linux
sudo apt install -y openjdk-17-jdk maven
```

### Database Tools

```bash
# PostgreSQL
# macOS:  brew install postgresql
# Windows: choco install postgresql
# Linux:  sudo apt install -y postgresql postgresql-contrib

# Redis
# macOS:  brew install redis
# Windows: choco install redis-64
# Linux:  sudo apt install -y redis-server
```

## Step 3: Configure Git

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main

# Useful aliases
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --decorate"
```

## Step 4: Set Up Your IDE

We support **VS Code** and **IntelliJ / PyCharm**. See our dedicated guides:

- [VS Code setup](../install-and-setup/installing-and-setting-up-vscode.md)
- [PyCharm setup](../install-and-setup/installing-and-setting-up-pycharm.md)

### VS Code Quick Setup

```bash
code --install-extension ms-python.python
code --install-extension esbenp.prettier-vscode
code --install-extension redhat.vscode-yaml
code --install-extension GitHub.copilot
```

Create `.vscode/settings.json` in your workspace:

```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.organizeImports": true
  },
  "editor.rulers": [80, 120],
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true
}
```

## Step 5: Docker

Docker is useful for running databases and services without installing them natively.

1. Download [Docker Desktop](https://www.docker.com/products/docker-desktop) (macOS/Windows) or follow the [Docker Engine install](https://docs.docker.com/engine/install/) for Linux
2. Start Docker Desktop
3. Verify the installation:

```bash
docker --version
docker run hello-world
```

Pull base images we use across projects:

```bash
docker pull node:18-alpine
docker pull python:3.11-slim
docker pull postgres:14
docker pull redis:7-alpine
```

## Step 6: Database Quick Start

### PostgreSQL

```bash
# Start the service
# macOS:  brew services start postgresql
# Linux:  sudo systemctl start postgresql && sudo systemctl enable postgresql

# Create a development database
createdb devdb

# Connect and create a dev user
psql postgres
```

```sql
CREATE USER devuser WITH ENCRYPTED PASSWORD 'devpassword';
GRANT ALL PRIVILEGES ON DATABASE devdb TO devuser;
ALTER USER devuser CREATEDB;
\q
```

### Redis

```bash
# macOS:  brew services start redis
# Linux:  sudo systemctl start redis-server && sudo systemctl enable redis-server

# Test
redis-cli ping   # should return PONG
```

## Step 7: Verify Everything

```bash
echo "=== Tool Versions ==="
git --version
node --version
npm --version
python3 --version
docker --version

# Optional — if you installed them
java -version 2>&1 || echo "Java not installed"
mvn --version 2>&1 || echo "Maven not installed"
psql --version 2>&1 || echo "PostgreSQL not installed"
redis-cli --version 2>&1 || echo "Redis not installed"
```

## Test Your Setup

Clone one of our template repos and run it locally:

```bash
git clone https://github.com/EndToEndLabCR/template-api-python.git
cd template-api-python
python3 -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
uvicorn app.main:app --reload
```

In another terminal:

```bash
curl http://localhost:8000/health
```

If you get a healthy response, you're ready to go.

## Troubleshooting

### Port Conflicts

```bash
# Check what's using common ports
lsof -i :3000   # React dev server
lsof -i :8000   # FastAPI / Django
lsof -i :8080   # Spring Boot
lsof -i :5432   # PostgreSQL
lsof -i :6379   # Redis

# Kill a process if needed
kill -9 <PID>
```

### Docker Permission Issues (Linux)

```bash
sudo usermod -aG docker $USER
# Log out and log back in
```

### PATH Issues

```bash
echo $PATH
# Reload your shell
source ~/.zshrc   # or ~/.bashrc
```

See our [FAQ & Troubleshooting](../faq-and-troubleshooting/common-errors.md) section for more common issues.

## Next Steps

1. Follow the [Onboarding Guide](./onboarding-guide.md) if you haven't already
2. Read the [Git & GitHub Guide](./git-github-guide.md) to learn our workflow
3. Clone a project repo and make your first contribution
4. Join the [Discord community](https://discord.gg/mAD7Y6fNzv) and say hello

## Keeping Things Fresh

```bash
# macOS
brew update && brew upgrade

# Linux
sudo apt update && sudo apt upgrade

# Python (upgrade dependencies)
pip install --upgrade -r requirements.txt
```
