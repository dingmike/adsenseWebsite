---
title: "Claude Code Plugins: The Complete Guide to Installing, Managing, and Creating Extensions"
weight: 1
draft: false
tags: ["AI", "claude code", "agent"]
---


## Introduction

Remember the first time you discovered VS Code extensions? Install a few plugins, and your bare-bones editor transformed into a full-featured development environment.

Claude Code's plugin system is doing the same thing for AI-assisted programming — but on a much bigger scale. With over 9,000 plugins available in 2026, the ecosystem covers everything from code review and database queries to deployment automation and browser testing. A single plugin can bundle slash commands, AI agents, event-driven hooks, and external tool connections into one installable package.

This guide covers everything you need to know: how to discover and install plugins, manage your plugin collection, and even create your own. Whether you are new to Claude Code or looking to go deeper, there is something here for you.

## What Are Claude Code Plugins?

A Claude Code plugin is a **self-contained package of extensions** that adds new capabilities to your AI coding assistant. Before plugins existed, extending Claude Code meant manually configuring MCP servers, writing skills in separate directories, and copying hook configurations between projects. Plugins solve the distribution problem: install once, get everything, share with your team.

A plugin can include multiple components:

**Skills**: Markdown files with instructions that teach Claude how to handle specific tasks. Claude loads them automatically when relevant, or you can invoke them with `/plugin-name:skill-name`. Skills consume only 30-50 tokens each until needed.

**Subagents**: Specialized AI agents that run in isolated contexts for complex multi-step tasks. You can launch multiple agents in parallel.

**Hooks**: Event-driven automation scripts that fire at specific moments — auto-format after every file edit, run the linter before commits, or send a Slack notification on deploy.

**MCP Servers**: Model Context Protocol servers that connect Claude to external tools and services. This is the most powerful component — it gives Claude access to databases, APIs, browsers, and more.

**LSP Servers**: Language Server Protocol support for real-time code intelligence — go-to-definition, find references, live diagnostics.

Think of a plugin as an all-in-one toolkit: install one plugin and you get multiple skills, agents, hooks, and tool connections, all carefully composed to work together out of the box.

## How to Discover and Install Plugins

### Open the Plugin Manager

In any Claude Code session, type `/plugin` to open the interactive plugin manager. It has four tabs:

- **Discover**: Browse available plugins from all your marketplaces
- **Installed**: View and manage installed plugins
- **Marketplaces**: Add, remove, or update marketplace registries
- **Errors**: View any plugin loading errors

You can also browse plugins in your browser at claude.com/plugins.

### Official Marketplace Is Pre-Configured

The official Anthropic marketplace (`claude-plugins-official`) comes pre-configured when you install Claude Code — no setup needed. Install plugins directly:

```
/plugin install github@claude-plugins-official
```

This installs the GitHub integration plugin, giving Claude direct access to your repositories, issues, and pull requests.

### Add More Marketplaces

Beyond the official marketplace, you can add community and team marketplaces from multiple sources:

**GitHub repositories (most common)**:
```
/plugin marketplace add anthropics/claude-code
```

**Other Git hosts**:
```
/plugin marketplace add https://gitlab.com/company/plugins.git
```

**Local directories (for development)**:
```
/plugin marketplace add ./my-marketplace
```

**Remote URLs**:
```
/plugin marketplace add https://example.com/marketplace.json
```

After adding, run `/plugin marketplace list` to confirm the marketplace is active.

### Install a Plugin

**Via the interactive UI**: Open `/plugin`, go to the Discover tab, browse plugins, select one, and choose your installation scope.

**Via direct command**:
```
/plugin install plugin-name@marketplace-name
```

Target a specific marketplace:
```
/plugin install commit-commands@anthropics-claude-code
```

### Three Installation Scopes

Plugins can be installed at three scopes:

- **User scope** (default): Available in all projects on your machine. Config stored in `~/.claude/settings.json`
- **Project scope**: Available only in the current project. Config stored in `.claude/settings.json` — share with your team via version control
- **Local scope**: Current project only, gitignored. For personal debugging

Specify scope via CLI:
```
claude plugin install formatter@my-marketplace --scope project
```

## Managing Your Plugins

### Daily Management

**List installed plugins**:
```
/plugin list
```
Or as JSON:
```
claude plugin list --json
```

**Disable and re-enable** (without uninstalling):
```
/plugin disable plugin-name@marketplace-name
/plugin enable plugin-name@marketplace-name
```

**Uninstall completely**:
```
/plugin uninstall plugin-name@marketplace-name
```

**Important**: After any changes, run `/reload-plugins` to apply them without restarting the session. Claude Code reports everything it loaded — skills, agents, hooks, MCP servers, and LSP servers.

### Manage Marketplaces

```
/plugin marketplace list              # List all marketplaces
/plugin marketplace update name       # Refresh a marketplace
/plugin marketplace remove name       # Remove a marketplace
```

Auto-updates are on by default for the official marketplace and off for third-party ones. Toggle this in the `/plugin` Marketplaces tab.

## Recommended Plugins to Install

### The Essential Three

**Feature Dev (Anthropic)**: Structured 7-phase development workflow — discovery, codebase exploration, architecture design, implementation, quality review. One of the highest-installed plugins.
```
/plugin install feature-dev@claude-plugins-official
```

**Code Review (Anthropic)**: Multi-agent code review across four dimensions — security, performance, maintainability, and correctness. Results ranked by confidence.
```
/plugin install code-review@claude-plugins-official
```

**Context7 (Upstash)**: Real-time documentation lookup. Claude's training data has a cutoff date — Context7 pulls current docs directly from source repositories.
```
/plugin install context7@claude-plugins-official
```

### For Frontend Developers

**Frontend Design**: Design system skills that produce high-quality UI code. Over 96,000 installs.
```
/plugin install frontend-design@claude-plugins-official
```

### MCP Server Plugins

MCP servers are the most powerful plugin component — they connect Claude to external services:

- **GitHub MCP**: Search repos, manage issues and PRs, interact with GitHub APIs
- **PostgreSQL MCP**: Natural language database queries with schema inspection
- **Playwright MCP**: Browser automation for end-to-end testing
- **File System MCP**: Sandboxed local file operations

Install MCP servers:
```
claude mcp add github -- npx -y @modelcontextprotocol/server-github
```

### For Teams

**Hookify (Anthropic)**: Visual hook configuration tool. Set up automation rules without manually editing config files.
```
/plugin install hookify@claude-plugins-official
```

## Best Practices

### Less Is More

Every plugin adds context overhead. Twenty plugins competing for attention will perform worse than a focused set of 5-7. Start with the essentials and add as needed.

Recommended starter setup:
- 3 core plugins: Feature Dev + Code Review + Context7
- 2-3 MCP servers: GitHub + stack-specific
- 1-2 custom skills: team coding standards, deployment procedure

### Choose the Right Scope

- **Personal plugins** → User scope
- **Team workflow plugins** → Project scope (committed to `.claude/settings.json`, auto-syncs for teammates)
- **Experimental plugins** → Local scope

### Preview Before Installing

Community plugins are plain text. Read the SKILL.md before installing to understand exactly what instructions they inject. Vague instructions produce vague results.

### Develop with --plugin-dir

When building your own plugin, test locally with:
```
claude --plugin-dir ./my-plugin
```
After modifications, run `/reload-plugins` to pick up changes without restarting.

## Create Your Own Plugin

Creating a Claude Code plugin is surprisingly simple. The simplest plugin is a single Markdown file; the most complex can bundle skills, agents, hooks, and MCP servers.

Basic structure:

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json        # Manifest: name, version, description
├── skills/                 # Skill directories
│   └── hello/
│       └── SKILL.md
└── README.md
```

Write the `plugin.json` manifest:
```json
{
  "name": "my-first-plugin",
  "version": "1.0.0",
  "description": "My first Claude Code plugin"
}
```

Create a skill (`skills/hello/SKILL.md`):
```markdown
---
name: hello
description: A simple greeting skill
---

# Hello Skill

This is an example skill. After installation, invoke it with `/my-first-plugin:hello`.
```

Test locally:
```
claude --plugin-dir ./my-plugin
```

When ready, push to GitHub and distribute through a marketplace.

**Critical**: Only `plugin.json` goes inside `.claude-plugin/`. All component directories (`skills/`, `agents/`, `hooks/`, etc.) must be at the plugin root level.

### Troubleshooting Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| Plugin not loading | Invalid plugin.json | Run `claude plugin validate` or `/plugin validate` |
| Skills not appearing | Wrong directory structure | Ensure `skills/` is at plugin root, not inside `.claude-plugin/` |
| Hooks not firing | Script not executable | Run `chmod +x script.sh` |
| MCP server fails | Missing `CLAUDE_PLUGIN_ROOT` | Use `$CLAUDE_PLUGIN_ROOT` for all plugin paths |
| `/plugin` command missing | Claude Code outdated | Update to version 1.0.33 or later |

## Summary

Claude Code's plugin ecosystem transforms AI-assisted programming from a chat tool into a complete development platform. With plugins, you can:

- **Extend capabilities**: Connect databases, APIs, browsers, and more
- **Standardize workflows**: Package team best practices as reusable skills
- **Automate actions**: Fire hooks at critical moments
- **Share with teams**: Distribute configurations with one command

With 9,000+ plugins, a pre-configured official marketplace, and single-command installation — there has never been a better time to explore the Claude Code plugin ecosystem.

Open your terminal, type `/plugin`, and transform your development workflow.

Official docs: https://code.claude.com/docs/en/overview
Plugin marketplace: https://claude.com/plugins
GitHub repo: https://github.com/anthropics/claude-code
