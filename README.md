# Go Code Editing Agent

A ready-to-run coding agent built in Go that uses Claude AI to interact with files and execute coding tasks. OCR via Tesseract is included as an optional bonus.

## Overview

This project demonstrates how to build an AI agent capable of:
- Reading and listing files in the workspace
- Editing files through natural language instructions
- Creating new files and directories
- Understanding and executing multi-step coding tasks

If you want a quick, out-of-the-box coding agent, this repo is the fastest path. If you want to learn how it works and how to build your own, the [How to Build an Agent](https://ampcode.com/notes/how-to-build-an-agent) guide explains it clearly and is highly recommended.

## Features

- **Interactive Chat Interface**: Chat with Claude AI directly in your terminal
- **File Operations**: The agent can read, list, and edit files in your workspace
- **Tool Use**: Claude automatically determines when to use tools based on your requests
- **Context-Aware**: Maintains conversation history for multi-turn interactions

## Available Tools

- `read_file`: Read the contents of any file
- `list_files`: List files and directories at a given path
- `edit_file`: Make edits to text files using string replacement
- `ocr_pdf`: OCR a PDF using `pdftoppm` + Tesseract (optional)

### Working with Different Directories

The agent can access files and directories anywhere on your system, not just the current working directory. You can use:

**Relative paths:**
- `../other-folder/file.txt` - Access parent directory
- `subfolder/document.pdf` - Access subdirectory
- `../../documents/report.pdf` - Navigate multiple levels

**Absolute paths:**
- `/home/username/documents/file.txt` (Linux/macOS)
- `C:\Users\username\documents\file.txt` (Windows/WSL)

**Examples:**
```
You: List files in /home/username/Documents
You: Read the file at ../project/config.json
You: OCR the PDF at /home/username/Downloads/invoice.pdf
```

## Prerequisites

- [Go](https://go.dev/) 1.24.1 or later
- [Anthropic API key](https://console.anthropic.com/settings/keys)
- Optional OCR: `tesseract` and `pdftoppm` (Poppler)

### Installing OCR Dependencies (Optional)

The OCR functionality requires two tools: `tesseract` (for text recognition) and `pdftoppm` (from Poppler, for PDF rendering). These are only needed if you want to use the `ocr_pdf` tool.

#### Linux (Ubuntu/Debian/WSL)
```bash
sudo apt-get update
sudo apt-get install poppler-utils tesseract-ocr
```

#### Linux (Fedora/RHEL/CentOS)
```bash
sudo dnf install poppler-utils tesseract
```

#### macOS
Using Homebrew:
```bash
brew install poppler tesseract
```

If you don't have Homebrew installed:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### Windows

**Option 1: Using Chocolatey**
```powershell
choco install poppler tesseract
```

**Option 2: Manual Installation**
1. **Poppler (pdftoppm):**
   - Download from: https://github.com/oschwartz10612/poppler-windows/releases
   - Extract and add the `bin` folder to your PATH

2. **Tesseract:**
   - Download from: https://github.com/UB-Mannheim/tesseract/wiki
   - Install and add to your PATH

#### Verify Installation
After installation, verify both tools are accessible:
```bash
pdftoppm -v
tesseract --version
```

**Optional Language Packs:**
For OCR support in languages other than English:
```bash
# Linux/WSL
sudo apt-get install tesseract-ocr-[language-code]

# macOS
brew install tesseract-lang

# Examples: tesseract-ocr-spa (Spanish), tesseract-ocr-fra (French)
```

## Setup

1. Clone this repository:
```bash
git clone https://github.com/BillStewRod/Go-code-editing-agent.git
cd Go-code-editing-agent
```

2. Set your Anthropic API key as an environment variable:
```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```

3. Install dependencies:
```bash
go mod tidy
```

## Usage

Run the agent:
```bash
go run main.go
```

Once running, you can interact with Claude by typing natural language commands:

- "What files are in this directory?"
- "Read main.go and explain what it does"
- "Create a new file called hello.js with a hello world function"
- "Edit the file to change X to Y"

Press `Ctrl+C` to exit.

## Example Interactions

```
You: What Go files are in this directory?
Claude: [uses list_files tool, then reads each Go file]

You: Create a fizzbuzz.js file
Claude: [creates the file with proper FizzBuzz implementation]

You: Edit that file to only run until 15
Claude: [reads the file, then edits it accordingly]
```

## How It Works

The agent operates on a simple but powerful loop:

1. Accept user input
2. Send conversation history to Claude along with available tool definitions
3. If Claude requests a tool use, execute it and return the result
4. Display Claude's response and repeat

The magic is that Claude 3.7 Sonnet is trained to understand when and how to use tools, making the implementation surprisingly straightforward.

## Project Structure

- `main.go`: Complete agent implementation including:
  - Agent loop and conversation management
  - Tool definitions and execution
  - File system operations

## Learn More

If you are curious about building agents, start with [How to Build an Agent](https://ampcode.com/notes/how-to-build-an-agent). It walks through the concepts clearly. But if you just want a quick out-of-the-box coding agent, use this repo.

## License

MIT
