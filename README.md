# codeWithClaude

A comprehensive guide to setting up and using Claude Code with Ollama for local AI-powered coding assistance.

## 📋 Overview

Claude Code is Anthropic's agentic coding tool that can read, modify, and execute code in your working directory. This repository provides step-by-step instructions to set up Claude Code with Ollama, enabling you to use open-source models locally for AI-assisted development.

## 🚀 Prerequisites

- macOS, Linux, or Windows
- Terminal/Command Line access
- Stable internet connection for initial setup

---

## 📦 Installation Steps

### Step 1: Install Ollama

Ollama is required to run local language models that Claude Code can use.


#### For Windows/Mac/Linux:

Download and install Ollama from [https://ollama.ai/download](https://ollama.ai/download)

#### Verify Installation:

```bash
ollama --version
```

---

### Step 2: Install Claude Code

Install Claude Code using the official installation script:

#### For macOS & Linux:

```bash
irm https://claude.ai/install.ps1 | iex
```

#### Verify Installation:

After installation, verify that Claude Code is installed correctly by checking the version:

```bash
claude --version
```

---

### Step 3: Pull Recommended Models

Download one or more recommended models to use with Claude Code. Choose based on your system capabilities:

**Recommended Models:**

```bash
# For systems with 16GB+ RAM
ollama pull qwen3-coder

# Lightweight and fast (recommended for most users)
ollama pull glm-4.7

# Balanced option (20B parameters)
ollama pull gpt-oss:20b

# More capable but resource-intensive (120B parameters)
ollama pull gpt-oss:120b
```

**Note:** Start with `glm-4.7` or `gpt-oss:20b` if you're unsure about your system's capabilities.

---

### Step 4: Integrate Ollama with Claude Code

<!-- ADD YOUR INTEGRATION STEPS HERE -->

---

## 🎯 Usage with Ollama

### Quick Setup

Launch Claude Code with Ollama:

```bash
ollama launch claude
```

### Configure Without Launching

To configure Claude Code without immediately launching it:

```bash
ollama launch claude --config
```

### Manual Setup

Claude Code connects to Ollama using the Anthropic-compatible API.

#### 1. Set Environment Variables:

```bash
export ANTHROPIC_AUTH_TOKEN=ollama
export ANTHROPIC_API_KEY=""
export ANTHROPIC_BASE_URL=http://localhost:11434
```

#### 2. Run Claude Code with an Ollama Model:

```bash
claude --model gpt-oss:20b
```

Or run with environment variables inline:

```bash
ANTHROPIC_AUTH_TOKEN=ollama ANTHROPIC_BASE_URL=http://localhost:11434 claude --model gpt-oss:20b
```

---

## 💡 Example Usage

Once Claude Code is running, you can ask it to help with various coding tasks:

```bash
# Create a simple web application
add a hello world website

# Analyze existing code
review the code in this directory

# Debug and fix issues
find and fix bugs in main.py

# Generate new features
add a login page with authentication
```

---

## ⚙️ Configuration

### Context Window

Claude Code requires a large context window. It's recommended to use at least 64k tokens.

To adjust context length in Ollama, refer to the [context length documentation](https://github.com/ollama/ollama/blob/main/docs/faq.md#how-can-i-specify-the-context-window-size).

### Model Selection

Choose your model based on your hardware:

| Model | Size | RAM Required | Best For |
|-------|------|--------------|----------|
| glm-4.7 | ~3-4GB | 8GB+ | Quick tasks, fast responses |
| gpt-oss:20b | ~10-14GB | 16GB+ | Balanced performance |
| qwen3-coder | ~49GB | 64GB+ | Advanced coding tasks |
| gpt-oss:120b | ~60GB+ | 128GB+ | Maximum capability |

---

## 🛠️ Troubleshooting

### Ollama Not Running

If you get connection errors, ensure Ollama is running:

```bash
ollama serve
```

### Model Not Found

Pull the model before using it:

```bash
ollama pull <model-name>
```
### List Models

Before pulling the models check any models you have installed using:

```bash
ollama pull <model-name>
```

### Memory Issues

If you experience crashes or slowdowns:
- Use a smaller model (glm-4.7)
- Close other applications
- Increase system swap space

---

## 📚 Additional Resources

- [Ollama Documentation](https://github.com/ollama/ollama)
- [Claude Code Documentation](https://docs.claude.ai)
- [Available Ollama Models](https://ollama.com/search?c=cloud)
- [Anthropic API Documentation](https://docs.anthropic.com)

---

## 🔧 Advanced Troubleshooting

### Common Installation Issues

#### Windows Installation Issues: Errors in WSL

If you're using Windows Subsystem for Linux (WSL), you might encounter the following issues:

##### 1. OS/Platform Detection Issues

If you receive an error during installation, WSL may be using Windows `npm`. Try:

**Solution:**
- Run `npm config set os linux` before installation
- Install with: `npm install -g @anthropic-ai/claude-code --force --no-os-check` (Do NOT use `sudo`)

##### 2. Node Not Found Errors

If you see `exec: node: not found` when running `claude`, your WSL environment may be using a Windows installation of Node.js.

**Check with:**
```bash
which npm
which node
```

These should point to Linux paths starting with `/usr/` rather than `/mnt/c/`.

**Solution:**
Install Node via your Linux distribution's package manager or via `nvm`:

```bash
# Using nvm (recommended)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc
nvm install --lts
```

##### 3. NPM Version Conflicts

If you have npm installed in both WSL and Windows, you may experience version conflicts when switching Node versions in WSL. This happens because WSL imports the Windows PATH by default, causing Windows nvm/npm to take priority over the WSL installation.

**Solution: Native Claude Code Installation (Recommended)**

Claude Code has a native installation that doesn't depend on npm or Node.js.

**For macOS, Linux, WSL:**

```bash
# Install stable version (default)
curl -fsSL https://claude.ai/install.sh | bash

# Install latest version
curl -fsSL https://claude.ai/install.sh | bash -s latest

# Install specific version number
curl -fsSL https://claude.ai/install.sh | bash -s 1.0.58
```

**For Windows PowerShell:**

```powershell
# Install stable version (default)
irm https://claude.ai/install.ps1 | iex

# Install latest version
& ([scriptblock]::Create((irm https://claude.ai/install.ps1))) latest

# Install specific version number
& ([scriptblock]::Create((irm https://claude.ai/install.ps1))) 1.0.58
```

#### Windows: "installMethod is native, but claude command not found"

If you see this error after installation, the `claude` command isn't in your PATH.

**Solution: Add to PATH manually**

1. **Open Environment Variables:**
   - Press `Win + R`, type `sysdm.cpl`, and press Enter
   - Click **Advanced** → **Environment Variables**

2. **Edit User PATH:**
   - Under "User variables", select **Path** and click **Edit**
   - Click **New** and add:
     ```
     %USERPROFILE%\.Local\bin
     ```

3. **Restart Your Terminal:**
   - Close and reopen PowerShell or CMD for changes to take effect

**Verify Installation:**

```bash
claude doctor  # Check installation health
```

---

## 📖 Reference Documentation

For more detailed troubleshooting and solutions, visit the official [Claude Code Troubleshooting Guide](https://code.claude.com/docs/en/troubleshooting).

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

## 📄 License

This project is provided as-is for educational purposes.

---

## ⭐ Acknowledgments

- [Anthropic](https://anthropic.com) for Claude Code
- [Ollama](https://ollama.ai) for local model hosting
- Open source community for the models

---

**Happy Coding with Claude! 🚀**

**~Arjya**