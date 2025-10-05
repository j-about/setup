# Windows Setup

Setup guide for Windows with **WSL2**.

## Table of Contents
- [Prerequisites](#prerequisites)
- [WSL2 Setup](#wsl2-setup)
- [Debian Configuration](#debian-configuration)
  - [System Update](#system-update)
  - [GitHub CLI Repository](#github-cli-repository)
  - [Essential Command-line Tools Installation](#essential-command-line-tools-installation)
  - [Homebrew Installation](#homebrew-installation)
  - [Oh My Zsh Installation & Configuration](#oh-my-zsh-installation--configuration)
  - [Default Browser Configuration](#default-browser-configuration)
- [Git and GitHub Setup](#git-and-github-setup)
  - [GitHub Authentication](#github-authentication)
  - [Git Configuration](#git-configuration)
- [Environment Variable Management](#environment-variable-management)
  - [direnv Installation](#direnv-installation)
- [Python Package Management (uv)](#python-package-management-uv)
- [Node.js and npm](#nodejs-and-npm)
  - [Node.js Installation](#nodejs-installation)
  - [npm Global Configuration](#npm-global-configuration)
  - [ESLint Installation](#eslint-installation)
- [Node.js Version Manager (fnm)](#nodejs-version-manager-fnm)
- [DevOps Tools](#devops-tools)
  - [Ansible Installation](#ansible-installation)
  - [Google Cloud CLI Installation](#google-cloud-cli-installation)
  - [Supabase CLI Installation](#supabase-cli-installation)
- [Visual Studio Code Extensions](#visual-studio-code-extensions)
- [Artificial Intelligence](#artificial-intelligence)
  - [Claude Code](#claude-code)
  - [OpenAI Codex CLI](#openai-codex-cli)
  - [Gemini CLI](#gemini-cli)

## Prerequisites
- **Windows 10 version 2004** or *higher*, or **Windows 11**
- Administrator privileges
- Internet connection
- **Brave Browser** installed from the [official website](https://brave.com/)
- **Docker Desktop** installed from the [official website](https://www.docker.com/)
- **Visual Studio Code** installed from the [official website](https://code.visualstudio.com/)

## WSL2 Setup

Open **Windows PowerShell** *as Administrator* and run:
```powershell
wsl --install -d Debian
```

## Debian Configuration

### System Update

Update the **Debian** system:
```bash
sudo apt update && sudo apt upgrade -y
```

### GitHub CLI Repository

Add the official **GitHub CLI repository** to **APT**:
```bash
(type -p wget >/dev/null || (sudo apt update && sudo apt-get install wget -y)) \
	&& sudo mkdir -p -m 755 /etc/apt/keyrings \
        && out=$(mktemp) && wget -nv -O$out https://cli.github.com/packages/githubcli-archive-keyring.gpg \
        && cat $out | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
	&& sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
	&& sudo mkdir -p -m 755 /etc/apt/sources.list.d \
	&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
```

### Essential Command-line Tools Installation

Install essential command-line tools including **Zsh** shell:
```bash
sudo apt install -y apt-transport-https build-essential ca-certificates curl git gh gnupg jq rsync tree unzip zsh
```

### Homebrew Installation

Install **Homebrew**:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Add **Homebrew** to your *PATH*:
```bash
echo >> ~/.zshrc
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.zshrc
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
```

Install **GCC** compiler:
```bash
brew install gcc
```

### Oh My Zsh Installation & Configuration

Install **Oh My Zsh**, a popular framework for configuring the **Zsh** shell:
```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Install the **zsh-syntax-highlighting** plugin:
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```

Edit the **Zsh** configuration file:
```bash
nano ~/.zshrc
```

Add the following plugins configuration:
```
plugins=(common-aliases git gitfast history-substring-search last-working-dir zsh-syntax-highlighting)
```

Apply changes by reloading the **Zsh** configuration file:
```bash
source ~/.zshrc
```

### Default Browser Configuration

Configure **Brave Browser** as your default browser for **WSL** integration:
```bash
echo "export BROWSER=\"/mnt/c/Program Files/BraveSoftware/Brave-Browser/Application/brave.exe\"" >> ~/.zshrc
echo "export GH_BROWSER=\"'/mnt/c/Program Files/BraveSoftware/Brave-Browser/Application/brave.exe'\"" >> ~/.zshrc
```

Apply changes by reloading the **Zsh** configuration file:
```bash
source ~/.zshrc
```

## Git and GitHub Setup

### GitHub Authentication

Authenticate with **GitHub**:
```bash
gh auth login -s 'user:email' -w
```

### Git Configuration

Configure **Git** with your email and username:
```bash
git config --global user.email "<EMAIL>"
git config --global user.name "<USERNAME>"
```

## Environment Variable Management

### direnv Installation

Install **direnv** for environment variable management:
```bash
curl -sfL https://direnv.net/install.sh | sudo bash
```

Enable **direnv** integration in **Zsh**:
```bash
echo 'eval "$(direnv hook zsh)"' >> ~/.zshrc
```

Apply changes by reloading the **Zsh** configuration file:
```bash
source ~/.zshrc
```

## Python Package Management (uv)

Install **uv** for *Python package management*:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## Node.js and npm

### Node.js Installation

Switch to **root** user:
```bash
sudo su
```

Download the **Node.js 22 (LTS)** repository setup script:
```bash
curl -fsSL https://deb.nodesource.com/setup_22.x -o nodesource_setup.sh
```

Execute the setup script:
```bash
bash nodesource_setup.sh
```

Install **Node.js 22 (LTS)**:
```bash
apt-get install -y nodejs
```

Exit root user:
```bash
exit
```

### npm Global Configuration

Create a directory for global installations:
```bash
mkdir -p ~/.npm-global/lib
```

Configure **npm** to use the new directory path:
```bash
npm config set prefix '~/.npm-global'
```

Add the global directory to *PATH*:
```bash
echo "export PATH=~/.npm-global/bin:$PATH" >> ~/.zshrc
```

Apply changes by reloading the **Zsh** configuration file:
```bash
source ~/.zshrc
```

### ESLint Installation

Install **ESLint** globally:
```bash
npm install -g eslint
```

## Node.js Version Manager (fnm)

Install **fnm** for *Node.js version management*:
```bash
curl -fsSL https://fnm.vercel.app/install | bash
```

Remove the global directory from *PATH*:
```bash
sed -i '/^export PATH=~\/.npm-global\/bin:\$PATH$/ {N;/\n$/d;}' ~/.zshrc
```

Add a **Zsh** hook that automatically uses the **Node.js** version from a project's *.node-version* file, or reverts to the system version if no file exists:
```bash
cat << 'EOF' >> ~/.zshrc
export NPM_GLOBAL_PATH="${HOME}/.npm-global"

setup_node_hook() {
  local current_dir="${PWD}"
  local node_version_file=""

  while [[ "${current_dir}" != "/" ]]; do
    if [[ -f "${current_dir}/.node-version" ]]; then
      node_version_file="${current_dir}/.node-version"
      break
    fi
    current_dir="$(dirname "${current_dir}")"
  done

  path=("${(@)path:#${NPM_GLOBAL_PATH}/bin}")
  path=("${(@)path:#/run/user/*/fnm_multishells/*}")
  export PATH="${(j/:/)path}"
  eval "$(fnm env)"

  if [[ -n "${node_version_file}" ]]; then
    echo "[setup node hook] .node-version file found at: ${node_version_file}"
    fnm use --install-if-missing "$(cat "${node_version_file}")"
    npm config delete prefix
    eval "$(fnm env --shell zsh)"
  else
    echo "[setup node hook] No .node-version found."
    fnm use system
    npm config set prefix "$NPM_GLOBAL_PATH"
    export PATH="${NPM_GLOBAL_PATH}/bin:${PATH}"
  fi
}

setup_node_hook

autoload -U add-zsh-hook
add-zsh-hook chpwd setup_node_hook
EOF
```

Apply changes by reloading the **Zsh** configuration file:
```bash
source ~/.zshrc
```

## DevOps Tools

### Ansible Installation
ℹ️ [Official documentation](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-debian)

Configure the **Ubuntu codename** and add the official **Ansible PPA** repository:
```bash
UBUNTU_CODENAME=jammy
wget -O- "https://keyserver.ubuntu.com/pks/lookup?fingerprint=on&op=get&search=0x6125E2A8C77F2818FB7BD15B93C4A3FD7BB9C367" | sudo gpg --dearmour -o /usr/share/keyrings/ansible-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/ansible-archive-keyring.gpg] http://ppa.launchpad.net/ansible/ansible/ubuntu $UBUNTU_CODENAME main" | sudo tee /etc/apt/sources.list.d/ansible.list
sudo apt update
```

Install **Ansible**:
```bash
sudo apt install ansible
```

### Google Cloud CLI Installation
ℹ️ [Official documentation](https://cloud.google.com/sdk/docs/install#deb)

Import the **Google Cloud** public key:
```bash
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg
```

Add the **gcloud CLI** distribution URI as a package source:
```bash
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
```

Update and install the **gcloud CLI**:
```bash
sudo apt-get update && sudo apt-get install google-cloud-cli
```

Initialize **gcloud** to get started:
```bash
gcloud init
```

### Supabase CLI Installation
ℹ️ [Official documentation](https://supabase.com/docs/guides/local-development/cli/getting-started?queryGroups=platform&platform=linux)

Install the **Supabase CLI**:
```bash
brew install supabase/tap/supabase
```

## Visual Studio Code Extensions

Install essential **VS Code** extensions:
```bash
code --install-extension ms-vscode-remote.remote-wsl
code --install-extension bradlc.vscode-tailwindcss
code --install-extension charliermarsh.ruff
code --install-extension dbaeumer.vscode-eslint
code --install-extension docker.docker
code --install-extension ecmel.vscode-html-css
code --install-extension esbenp.prettier-vscode
code --install-extension mechatroner.rainbow-csv
code --install-extension ms-azuretools.vscode-containers
code --install-extension ms-kubernetes-tools.vscode-kubernetes-tools
code --install-extension ms-ossdata.vscode-pgsql
code --install-extension ms-python.python
code --install-extension ms-python.vscode-pylance
code --install-extension ms-toolsai.jupyter
code --install-extension PKief.material-icon-theme
code --install-extension redhat.ansible
code --install-extension redhat.vscode-yaml
code --install-extension Supabase.vscode-supabase-extension
code --install-extension tamasfe.even-better-toml
```

## Artificial Intelligence

### Claude Code

Install **Claude Code**:
```bash
npm install -g @anthropic-ai/claude-code
npm install -g ccusage
```

Initialize **Claude Code** configuration:
```bash
claude
```

Add *MCP servers* to **Claude Code**:
```bash
claude mcp add -s user context7 -- npx -y @upstash/context7-mcp
claude mcp add -s user -t http deepwiki https://mcp.deepwiki.com/mcp
claude mcp add -s user ESLint -- npx -y @eslint/mcp@latest
claude mcp add -s user taskmaster-ai -e OPENAI_API_KEY=<OPENAI_API_KEY> PERPLEXITY_API_KEY=<PERPLEXITY_API_KEY> -- npx -y --package=task-master-ai task-master-ai
claude mcp add -s user perplexity-ask -e PERPLEXITY_API_KEY=<PERPLEXITY_API_KEY> -- npx -y server-perplexity-ask
```

Install the **Claude Code for VS Code** extension:
```bash
code --install-extension 	anthropic.claude-code
```

### OpenAI Codex CLI

Configure *OpenAI API key*:
```bash
echo "export OPENAI_API_KEY=\"<OPENAI_API_KEY>\"" >> ~/.zshrc
```

Apply changes by reloading the **Zsh** configuration file:
```bash
source ~/.zshrc
```

Install **OpenAI Codex CLI**:
```bash
npm install -g @openai/codex
```

Install the **Codex – OpenAI’s coding agent** extension for **Visual Studio Code**:
```bash
code --install-extension openai.chatgpt
```

### Gemini CLI

Install **Gemini CLI**:
```bash
npm install -g @google/gemini-cli
```

Initialize **Gemini** configuration:
```bash
gemini
```

Configure *MCP servers* for **Gemini CLI**:
```bash
nano .gemini/settings.json
```

Add the following configuration:
```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": [
        "-y",
        "@upstash/context7-mcp"
      ]
    },
    "deepwiki": {
      "httpUrl": "https://mcp.deepwiki.com/mcp"
    },
    "ESLint": {
      "command": "npx",
      "args": [
        "-y",
        "@eslint/mcp@latest"
      ]
    },
    "perplexity-ask": {
      "command": "npx",
      "args": [
        "-y",
        "server-perplexity-ask"
      ],
      "env": {
        "PERPLEXITY_API_KEY": "<PERPLEXITY_API_KEY>"
      }
    },
    "taskmaster-ai": {
      "command": "npx",
      "args": [
        "-y",
        "--package=task-master-ai",
        "task-master-ai"
      ],
      "env": {
        "ANTHROPIC_API_KEY": "<ANTHROPIC_API_KEY>",
        "OPENAI_API_KEY": "<OPENAI_API_KEY>",
        "PERPLEXITY_API_KEY": "<PERPLEXITY_API_KEY>"
      }
    }
  }
}
```