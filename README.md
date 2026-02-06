# Go Code Editing Agent

A fully functioning code-editing agent built in Go that uses Claude AI to interact with files and execute coding tasks.

## Overview

This project demonstrates how to build an AI agent capable of:
- Reading and listing files in the workspace
- Editing files through natural language instructions
- Creating new files and directories
- Understanding and executing multi-step coding tasks

Built following the tutorial from [How to Build an Agent](https://ampcode.com/notes/how-to-build-an-agent), this agent showcases how LLMs can be given "tools" to interact with the file system and perform real coding work.

## Features

- **Interactive Chat Interface**: Chat with Claude AI directly in your terminal
- **File Operations**: The agent can read, list, and edit files in your workspace
- **Tool Use**: Claude automatically determines when to use tools based on your requests
- **Context-Aware**: Maintains conversation history for multi-turn interactions

## Available Tools

- `read_file`: Read the contents of any file
- `list_files`: List files and directories at a given path
- `edit_file`: Make edits to text files using string replacement

## Prerequisites

- [Go](https://go.dev/) 1.24.1 or later
- [Anthropic API key](https://console.anthropic.com/settings/keys)

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

This project is based on the excellent tutorial: [How to Build an Agent](https://ampcode.com/notes/how-to-build-an-agent)

The tutorial demonstrates that building a powerful AI agent doesn't require complex architectures or secret techniques—just an LLM, a loop, and the right tools.

## License

MIT
