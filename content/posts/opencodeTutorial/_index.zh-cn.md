---
title: "OpenCode 完全指南：安装配置到高效使用，10 分钟上手终端 AI 编程助手"
weight: 1
draft: false
description: "OpenCode 完全指南：安装配置到高效使用，10 分钟上手终端 AI 编程助手"
tags: ["AI", "vibe coding", "Open Code" ]
---

![Everything Claude Code](featured.png "Everything OpenCode")
-----

## 一、引子

想象这个场景：你坐在终端前，输入 `opencode "给用户注册接口加上 JWT 认证"`，然后看着一个 AI 代理读取你的整个代码库，规划出实现方案，编写代码，运行测试，最后创建了一个完美的 PR——而你只需要审阅结果。

这不是 demo 视频，这是 OpenCode 的日常。

OpenCode 是 GitHub 上增长最快的开源 AI 编程代理，已获得超过 12 万颗星标。它用 Go 语言构建，直接运行在你的终端里，能够理解整个项目，可以通过自然语言对话来编辑文件、执行命令、管理 Git，甚至是部署代码。

这篇教程会带你从零开始，在 10 分钟内学会使用 OpenCode。

## 二、OpenCode 是什么

市面上有很多 AI 编程工具，OpenCode 有什么不同？

**它是真正的代理，不是聊天机器人。** 传统 AI 助手等你提问然后回答。OpenCode 会主动分析问题、制定计划、执行修改、验证结果——就像一个主动推进工作的资深工程师坐在你身边。

**它驻扎在终端里。** 不需要在浏览器标签页和编辑器之间来回切换。OpenCode 是你工作的地方的 AI。

**模型无关。** OpenCode 支持 75+ 个 LLM 提供商——Anthropic、OpenAI、Google Gemini、Groq，甚至通过 Ollama 使用本地模型。你可以在一次会话中用一条命令随时切换模型。

**真正的开源。** MIT 协议授权，可自行托管，你的数据不会离开你的基础设施。

## 三、安装：5 种方式任你选

OpenCode 支持 macOS、Linux 和 Windows（通过 WSL）。

### 方式一：快速安装脚本（推荐）

最快的方式，一条命令搞定：

```bash
curl -fsSL https://opencode.ai/install | bash
```

脚本会自动检测你的操作系统和架构，下载对应的二进制文件并配置到 PATH 中。无需任何依赖。

### 方式二：Homebrew（macOS / Linux）

如果你用 Homebrew，这是最干净的方式：

```bash
brew install anomalyco/tap/opencode
```

注意：官方 Homebrew 公式（`brew install opencode`）由 Homebrew 团队维护，更新较慢。上面的 OpenCode tap 始终保持最新版本。

### 方式三：npm（跨平台）

如果你的工作流中已经有 Node.js：

```bash
npm install -g opencode-ai
```

### 方式四：Docker（无需安装）

想在不安装任何东西到系统的情况下试用？

```bash
docker run -it --rm ghcr.io/anomalyco/opencode
```

### 方式五：平台特定安装

- **Arch Linux**：`sudo pacman -S opencode`（稳定版）或 `paru -S opencode-bin`（最新版）
- **Windows (Scoop)**：`scoop install opencode`
- **Windows (Chocolatey)**：`choco install opencode`
- **Go**：`go install github.com/anomalyco/opencode@latest`

### 验证安装

安装后确认一切正常：

```bash
opencode --version
```

你应该能看到类似 `v0.1.x` 的版本号。

## 四、配置：连接 AI 模型

OpenCode 是模型无关的——你选择想用的 AI 模型。

### 方案 A：OpenCode Zen（最简单）

对新手来说最简单的方式是 OpenCode Zen——一系列经过验证的模型集合：

1. 运行 `opencode` 启动 TUI
2. 输入 `/connect` 并选择 `opencode`
3. 在浏览器中打开 https://opencode.ai/auth
4. 登录后添加支付信息，复制 API key
5. 把 key 粘贴回终端

无需管理 API key，无需配置文件——开箱即用。

### 方案 B：使用你自己的 API Key

设置环境变量：

```bash
# Anthropic Claude
export ANTHROPIC_API_KEY="your-key-here"

# OpenAI
export OPENAI_API_KEY="your-key-here"

# Google Gemini
export GOOGLE_API_KEY="your-key-here"
```

把这几个加到 `~/.zshrc` 或 `~/.bashrc` 中永久生效。

### 方案 C：交互式认证

在命令行中运行：

```bash
opencode auth login
```

它会引导你选择提供商并设置凭证。凭证存储在 `~/.local/share/opencode/auth.json`。

## 五、第一次使用

### 启动 OpenCode

进入你的项目目录并启动：

```bash
cd /path/to/your/project
opencode
```

OpenCode 会启动它的终端用户界面（TUI）——一个运行在终端里的全屏聊天界面。

### 初始化项目

在 TUI 中运行：

```
/init
```

这会扫描你的项目结构，识别关键文件和模式，在项目根目录创建一个 `AGENTS.md` 文件。这个文件告诉 OpenCode 你的代码库的架构、约定和风格。

> 记得把 `AGENTS.md` 提交到 Git！你的整个团队都会受益于 OpenCode 理解项目上下文。

### 交给它一个任务

现在进入最有趣的部分。试试这个：

```
解释这个项目的架构
```

或者更有挑战性一点的：

```
给用户注册接口添加输入验证，包括邮箱格式和密码强度检查
```

OpenCode 会：
1. 读取相关文件
2. 制定计划（在 Plan 模式下显示）
3. 修改前请求你的确认
4. 实施解决方案
5. 运行测试验证

按 `Tab` 键切换 Plan 模式（仅建议，不修改文件）和 Build 模式（实际修改代码）。

## 六、核心命令速查

| 命令 | 说明 |
|---------|-------------|
| `/init` | 为当前项目初始化 OpenCode |
| `/connect` | 配置或切换 AI 提供商 |
| `/model` | 在会话中切换模型 |
| `/agents` | 列出和切换代理 |
| `opencode run "..."` | 非交互模式运行任务 |
| `opencode serve` | 启动 HTTP 服务器（OpenAPI） |
| `opencode models` | 列出可用模型 |
| `opencode auth login` | 交互式提供商认证 |

## 七、主要功能一览

### 双代理模式

OpenCode 内置两个代理：
- **代码代理**（默认）：在工作区中编辑代码
- **架构代理**：分析规划但不修改文件

按 `Tab` 键切换。复杂任务先用架构代理分析，再切换到代码代理实现。

### LSP 集成

OpenCode 连接到你项目的语言服务器协议（LSP），获得实时代码智能——跳转到定义、查找引用、实时诊断——支持 TypeScript、Python、Go、Rust 等语言。

### 多会话管理

OpenCode 跨会话跟踪你的对话历史。使用 `opencode sessions` 列出历史会话，随时继续之前的工作。

### 非交互模式

用于自动化和 CI/CD 流水线：

```bash
opencode run "把所有 console.log 替换为 logger 工具函数"
```

这种模式无头运行——不需要 TUI，没有交互提示。非常适合脚本自动化。

### MCP 服务器支持

OpenCode 支持模型上下文协议（Model Context Protocol），让 AI 连接外部工具，如数据库、API、文件系统。在项目配置 `opencode.json` 中配置 MCP 服务器。

## 八、实用技巧

**从小任务开始。** 先让 OpenCode 在一个明确的小问题上证明自己，再交给它大型重构任务。

**先审查计划。** 对复杂任务使用 Plan 模式（Tab 键）——计划阶段就能看出 OpenCode 是否理解了问题。

**改代码前先提交。** OpenCode 基于当前工作状态工作。干净的工作树能帮助它更清晰地推理变更。

**自定义 AGENTS.md。** `/init` 生成的文件只是一个起点。编辑它，加入项目特定的约定、API 文档和架构决策。

**用 `/model` 优化成本。** 复杂推理任务使用强力模型，简单任务切换成更便宜的模型，一次会话中随时切换。

## 九、总结

OpenCode 代表了一类新的开发工具——终端原生的 AI 编程代理。它开源、模型无关，深度集成在开发者已有的工作流程中。

10 分钟内，你可以从零到拥有一个理解你代码库、能写生产代码、能跑测试、能管理 Git 工作流的 AI 代理。入门门槛低得惊人：一条安装命令，一次 `/init`，然后你就开始高效工作了。

这个项目正在快速发展，拥有活跃的开源社区。无论你是一个想加速工作流的独立开发者，还是一个正在评估 AI 编程工具的团队，OpenCode 都值得你关注。

---

*官方网站：https://opencode.ai*
*GitHub 仓库：https://github.com/anomalyco/opencode*
*官方文档：https://dev.opencode.ai/docs*
