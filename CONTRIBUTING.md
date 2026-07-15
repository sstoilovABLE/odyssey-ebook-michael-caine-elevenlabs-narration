# Contributing

## Environment setup

1. Clone the repository and open it in your editor.
2. Install the required tools for editing and building the EPUB.
3. Run the project setup script for your environment.

In case you're using an agentic cloud workflow, here's the setup script for your Claude Code Cloud environment or Codex cloud environment:

```bash
#!/usr/bin/env bash
set -euo pipefail

echo "=== 1. Cleaning up restricted PPAs ==="
# Remove the problematic PPA files so apt doesn't attempt to reach them
sudo rm -f /etc/apt/sources.list.d/deadsnakes*.list
sudo rm -f /etc/apt/sources.list.d/ondrej*.list

echo "=== 2. Updating System Packages ==="
# Allow apt-get update to pass even if non-essential third-party repos fail
sudo apt-get update -y || true

echo "=== 3. Installing Core Tools & System Dependencies ==="
# Install essential packages available from the core Ubuntu repositories
sudo apt-get install -y \
    curl \
    git \
    default-jre \
    python3-dev \
    python3-pip \
    python3-venv \
    pipx

# Inject pipx binaries into the path globally for the environment
pipx ensurepath || true
export PATH="$HOME/.local/bin:$PATH"

echo "=== 4. Installing Standard Ebooks Toolset ==="
# Install the official toolset isolated using pipx
pipx install standardebooks --force

echo "=== 5. Preparing Node.js Environment ==="
# Install Node.js 22+ using NodeSource
curl -fsSL https://nodesource.com | sudo -E bash - || true
sudo apt-get update -y || true
sudo apt-get install -y nodejs
```
