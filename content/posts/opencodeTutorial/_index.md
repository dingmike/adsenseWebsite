---
title: " 🚀 OpenCode: The Complete Installation and Usage Tutorial"
weight: 1
draft: false
description: "OpenCode: The Complete Installation and Usage Tutorial."
tags: ["AI", "vibe coding", "Open Code" ]
---


![Everything Claude Code](featured.png "Everything OpenCode")
-----

## Introduction

Imagine this: you sit down at your terminal, type `opencode "Add user authentication with JWT"`, and watch as an AI agent reads your entire codebase, plans the implementation, writes the code, runs the tests, and creates a perfect pull request — all while you review the results.

This is not a demo video. This is OpenCode.

OpenCode is the fastest-growing open-source AI coding agent on GitHub, with over 120,000 stars. Built in Go, it runs directly in your terminal, understands your entire project, and can edit files, execute commands, manage git, and deploy code — all through natural language conversation.

This tutorial will take you from zero to productive in about 10 minutes.

## What Makes OpenCode Different?

There are many AI coding tools out there. What sets OpenCode apart?

**It's a true agent, not a chatbot.** Traditional AI assistants wait for you to ask a question, then reply. OpenCode actively analyzes problems, formulates plans, executes changes, and verifies results — like having a senior engineer working alongside you who takes initiative.

**It lives in your terminal.** No context-switching between browser tabs and your editor. OpenCode is the AI that meets you where you already work.

**Provider-agnostic.** OpenCode supports 75+ LLM providers — Anthropic, OpenAI, Google Gemini, Groq, and even local models through Ollama. You can switch providers mid-session with a single command.

**Truly open source.** Licensed under MIT, self-hostable, no data leaves your infrastructure unless you choose.

## Installation: 5 Ways to Get Started

OpenCode runs on macOS, Linux, and Windows (via WSL). Here are all the ways to install it:

### Method 1: Quick Install Script (Recommended)

The fastest way to get OpenCode running:

```bash
curl -fsSL https://opencode.ai/install | bash
```

This script detects your operating system and architecture, downloads the correct binary, and places it in your PATH. No dependencies required.

### Method 2: Homebrew (macOS / Linux)

If you use Homebrew, this is the cleanest option:

```bash
brew install anomalyco/tap/opencode
```

Note: The official Homebrew formula (`brew install opencode`) is maintained by the Homebrew team and updated less frequently. The OpenCode tap above always has the latest release.

### Method 3: npm (Cross-Platform)

If Node.js is already part of your workflow:

```bash
npm install -g opencode-ai
```

### Method 4: Docker (No Installation)

Want to try it out without installing anything on your host?

```bash
docker run -it --rm ghcr.io/anomalyco/opencode
```

### Method 5: Platform-Specific

- **Arch Linux**: `sudo pacman -S opencode` (stable) or `paru -S opencode-bin` (latest)
- **Windows (Scoop)**: `scoop install opencode`
- **Windows (Chocolatey)**: `choco install opencode`
- **Go**: `go install github.com/anomalyco/opencode@latest`

### Verify Installation

After installation, confirm everything works:

```bash
opencode --version
```

You should see a version number like `v0.1.x`.

## Configuration: Connect to an AI Provider

OpenCode is provider-agnostic — you choose the AI model you want to use.

### Option A: OpenCode Zen (Easiest)

The simplest path for new users is OpenCode Zen, a curated set of verified models:

1. Run `opencode` to start the TUI
2. Type `/connect` and select `opencode`
3. Head to https://opencode.ai/auth in your browser
4. Sign in, add billing details, and copy your API key
5. Paste the key back into the terminal

No API key management, no configuration files — just works.

### Option B: Bring Your Own API Key

Set environment variables for your preferred provider:

```bash
# Anthropic Claude
export ANTHROPIC_API_KEY="your-key-here"

# OpenAI
export OPENAI_API_KEY="your-key-here"

# Google Gemini
export GOOGLE_API_KEY="your-key-here"
```

Add these to your `~/.zshrc` or `~/.bashrc` to make them permanent.

### Option C: Interactive Auth

From the command line:

```bash
opencode auth login
```

This walks you through provider selection and credential setup interactively. Credentials are stored at `~/.local/share/opencode/auth.json`.

## Your First Session

### Start OpenCode

Navigate to a project directory and launch:

```bash
cd /path/to/your/project
opencode
```

OpenCode will start its Terminal User Interface (TUI) — a full-screen chat interface right in your terminal.

### Initialize for Your Project

Inside the TUI, run:

```
/init
```

This scans your project structure, identifies key files and patterns, and creates an `AGENTS.md` file in your project root. This file teaches OpenCode about your codebase — its architecture, conventions, and style.

> Commit your `AGENTS.md` to git! Your whole team will benefit from OpenCode understanding the project context.

### Give It a Task

Now the fun part. Try something like:

```
Explain the architecture of this project
```

Or something more ambitious:

```
Add input validation to the user registration endpoint
```

OpenCode will:
1. Read the relevant files
2. Formulate a plan (shown in Plan mode)
3. Ask for confirmation before making changes
4. Implement the solution
5. Run tests to verify

Press `Tab` to toggle between Plan mode (read-only suggestions) and Build mode (applies changes).

## Essential Commands Reference

| Command | Description |
|---------|-------------|
| `/init` | Initialize OpenCode for current project |
| `/connect` | Configure or switch AI provider |
| `/model` | Switch models mid-session |
| `/agents` | List and switch between agents |
| `opencode run "..."` | Run a task in non-interactive mode |
| `opencode serve` | Start an HTTP server (OpenAPI) |
| `opencode models` | List available models |
| `opencode auth login` | Interactive provider authentication |

## Key Features You Should Know

### Dual Agent Mode

OpenCode has two built-in agents:
- **Code Agent** (default): Edits code in your workspace
- **Architect Agent**: Analyzes and plans without touching files

Press `Tab` to switch between them. Use Architect first for complex tasks, then switch to Code to implement.

### LSP Integration

OpenCode connects to your project's Language Server Protocol (LSP) servers, giving it real-time code intelligence — go-to-definition, find references, live diagnostics — for languages like TypeScript, Python, Go, and Rust.

### Multi-Session Management

OpenCode tracks your conversation history across sessions. Use `opencode sessions` to list past sessions and pick up where you left off.

### Non-Interactive Mode

For automation and CI/CD pipelines:

```bash
opencode run "Refactor all console.log to use the logger utility"
```

This runs headless — no TUI, no interactive prompts. Perfect for scripts.

### MCP Server Support

OpenCode supports the Model Context Protocol, letting the AI connect to external tools like databases, APIs, and file systems. Configure MCP servers in your `opencode.json` project config.

## Pro Tips

**Start with small tasks.** Let OpenCode prove itself on a focused issue before handing it a major refactor.

**Review the plan first.** Use Plan mode (Tab) on complex tasks — the plan reveals whether OpenCode understood the problem before it starts writing code.

**Commit before asking for changes.** OpenCode works with your current state. A clean working tree helps it reason about changes clearly.

**Customize with AGENTS.md.** The `/init` generated file is a starting point. Edit it to add project-specific conventions, API documentation, and architectural decisions.

**Use `/model` to optimize costs.** Use a powerful model for complex reasoning and a cheaper model for simple tasks, switching mid-session.

## Summary

OpenCode represents a new category of development tool — the terminal-native AI coding agent. It's open source, provider-agnostic, and deeply integrated into the workflows developers already use.

In 10 minutes, you can go from nothing to having an AI agent that understands your codebase, writes production code, runs your tests, and manages your git workflow. The barrier to entry is remarkably low: one install command, one `/init`, and you're productive.

The project is evolving rapidly with an active open-source community. Whether you're a solo developer looking to accelerate your workflow or a team evaluating AI coding tools, OpenCode is worth your attention.

---

*Official website: https://opencode.ai*
*GitHub repository: https://github.com/anomalyco/opencode*
*Documentation: https://dev.opencode.ai/docs*
