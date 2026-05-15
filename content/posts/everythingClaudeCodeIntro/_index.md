---
title: "Everything Claude Code: The Ultimate Performance System for AI Agent Harnesses"
weight: 1
draft: false
tags: ["AI", "claude code", "agent", "plugin"]
---

> An Anthropic hackathon winner that grew into the most popular AI agent enhancement system—now with 174K+ GitHub stars.

---

## What Is Everything Claude Code?

**Everything Claude Code (ECC)** is an **agent harness performance optimization system**—a complete enhancement layer for AI coding agents like Claude Code, Codex, Cursor, OpenCode, and Gemini.

It started as a personal setup by [@affaan-m](https://github.com/affaan-m), who won the Anthropic x Forum Ventures hackathon building [zenith.chat](https://zenith.chat) entirely with Claude Code. After 10+ months of daily use building real products, he open-sourced his entire workflow. The result? A comprehensive system that has since accumulated **174,000+ stars** on GitHub and over **28,000 forks**.

ECC is **not** just a collection of config files. It's a complete, production-ready system:

- **300+ skills** — reusable prompt bundles for everything from code review to TDD to research
- **Instincts** — automatic behaviors that guide Claude's default responses
- **Memory optimization** — persistent knowledge graph for long-running projects
- **Continuous learning** — automated improvement loops that refine outputs over time
- **Security scanning** — built-in vulnerability detection for every commit
- **Research-first development** — automated multi-source research before code changes
- **MCP configurations** — ready-to-use Model Context Protocol server setups

And it's completely **free and MIT-licensed**.

---

## Why ECC Exists

If you've used Claude Code, you know it's powerful out of the box. But as you use it daily across real projects, you realize:

- You keep writing the same instructions
- Context windows fill up with setup boilerplate
- You spend time re-teaching Claude your conventions
- There's no built-in system for continuous improvement

ECC solves all of this by providing a **structured enhancement layer** that sits on top of your agent harness. Install it once, and suddenly your AI agent has:

- A complete library of specialized skills at its disposal
- Automatic memory of project conventions and decisions
- Built-in quality gates for security and code review
- Research capabilities that kick in before writing code

---

## Key Features

### Skills System

Skills are the primary workflow surface in ECC. They act like **scoped workflow bundles**: reusable prompts, structure, supporting files, and codemaps that let Claude quickly navigate your codebase without burning context on exploration.

Instead of describing what you want every time, you invoke a slash command:

```
/tdd          → Test-driven development workflow
/code-review  → Comprehensive code review
/e2e          → End-to-end testing setup
/refactor-clean → Dead code cleanup
/security-review → Security vulnerability scan
/deep-research → Multi-source research with synthesis
```

Each skill includes structured prompts, command handlers, and codemaps—everything Claude needs to execute that workflow correctly from the start.

### Instincts

Instincts are automatic behaviors that guide **how Claude responds by default**. Instead of starting from scratch each session, ECC configures instincts for:

- Code quality standards (immutability, error handling, naming conventions)
- Project-specific conventions (file organization, testing patterns)
- Security-first development (input validation, secret detection)
- Documentation discipline (when and how to document)

### Memory Optimization

ECC implements a **persistent knowledge graph** that tracks project entities, decisions, and relationships across sessions. This means your AI agent remembers:

- Architecture decisions and their rationale
- Which patterns work for your specific project
- Key entities and their relationships
- Past decisions that should inform future work

No more re-teaching Claude everything every session.

### Continuous Learning

ECC includes feedback loops that automatically improve outputs over time:

- Run evaluations to measure quality
- Detect patterns in past successes and failures
- Refine prompts and instincts based on results
- Build up a custom knowledge base for your domain

### Security Scanning

Before every commit, ECC can run a security scan that checks for:

- Hardcoded secrets and API keys
- SQL injection vulnerabilities
- XSS and CSRF patterns
- Insecure cryptographic usage
- Dependency vulnerabilities

### Research-First Development

ECC promotes a research-before-coding workflow. When you ask it to implement a feature, it automatically:

1. Searches existing code and GitHub for patterns
2. Checks library documentation via Context7
3. Synthesizes findings into a plan
4. Then—and only then—starts writing code

---

## Cross-Harness Compatibility

One of ECC's standout features is that it **works across multiple AI agent harnesses**. You're not locked into a single tool:

| Harness | Support |
|---------|---------|
| **Claude Code** | ✅ Full support |
| **Codex (OpenAI)** | ✅ Full support |
| **Cursor** | ✅ Full support |
| **OpenCode** | ✅ Full support |
| **Gemini** | ✅ Full support |
| **GitHub Copilot** | ✅ Support |

Install once, use everywhere.

---

## What's Inside

ECC contains a massive collection of production-tested components:

- **300+ skills** covering development, testing, security, research, and operations
- **100+ agents** for specialized tasks (code review, security, planning, research)
- **MCP server configurations** for Context7, Exa search, databases, GitHub, and more
- **Hooks system** for PostToolUse formatting, linting, and type checking
- **Language-specific rules** for TypeScript, Python, Go, Rust, Swift, PHP, and more
- **VSCode integration** and editor configurations
- **Plugin system** for seamless Claude Code integration
- **Template projects** for rapid bootstrapping

The project spans multiple languages—JavaScript (57%), Rust (33%), Python (5%), Shell (3%), and TypeScript (1%)—with 170+ contributors.

---

## How to Install

### Option 1: Install as Plugin (Recommended)

The easiest way is to install ECC as a Claude Code plugin:

```bash
# Add the marketplace
/plugin marketplace add https://github.com/affaan-m/everything-claude-code

# Install the plugin
/plugin install ecc@ecc
```

That's it. You now have access to all commands, agents, skills, and hooks.

### Option 2: Manual Installation

Clone the repo and copy what you need:

```bash
git clone https://github.com/affaan-m/everything-claude-code.git
cd everything-claude-code

# Copy rules for your tech stack (e.g., TypeScript + Web)
cp -r rules/typescript ~/.claude/rules/
cp -r rules/web ~/.claude/rules/
cp -r rules/common ~/.claude/rules/

# Copy skills you want
cp -r skills/* ~/.claude/skills/
```

### Option 3: Via settings.json

Add directly to your Claude configuration:

```json
{
  "extraKnownMarketplaces": {
    "ecc": {
      "source": {
        "source": "github",
        "repo": "affaan-m/everything-claude-code"
      }
    }
  },
  "enabledPlugins": {
    "ecc@ecc": true
  }
}
```

---

## Getting Started

Once installed, start with these commands:

```
/hookify        → Set up automation hooks for your project
/init           → Initialize ECC for your project
/tdd            → Start a test-driven development workflow
/code-review    → Review your current changes
/deep-research  → Research before implementing
```

Or dive into the shorthand guide: `/projects` shows project-level commands, `/plan` for structured feature planning.

---

## Why It Matters

AI coding agents are getting better at an astonishing rate, but raw model capability is only half the equation. The other half is **how you direct it**.

ECC provides the structure, memory, and workflow that transforms an AI agent from a clever autocomplete into a reliable, consistent development partner. It's the difference between asking Claude to "review this code" and having it check 15 specific quality gates across security, style, testing, and architecture.

With 174K+ stars and a thriving community of 170+ contributors, ECC has become the **de facto standard** for enhancing AI coding agents. It's not just a tool—it's a movement toward agentic development done right.

---

**Learn More:**

- GitHub: [github.com/affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code)
- Website: [ecc.tools](https://ecc.tools)
- License: MIT — free to use, modify, and share
