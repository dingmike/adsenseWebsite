---
title: "Everything Claude Code：AI 代理性能系统的终极方案能"
weight: 1
draft: false
tags: ["AI", "claude code", "agent", "plugin"]
---

> 一个源自 Anthropic 黑客马拉松获奖项目的 AI 代理增强系统，已获得 17.4 万+ GitHub 星标。

---

## 什么是 Everything Claude Code？

**Everything Claude Code（ECC）** 是一个**代理性能优化系统**——为 Claude Code、Codex、Cursor、OpenCode、Gemini 等 AI 编程代理提供完整的增强层。

它始于 [@affaan-m](https://github.com/affaan-m) 的个人工作流配置。作者完全使用 Claude Code 构建了 [zenith.chat](https://zenith.chat)，并赢得了 Anthropic x Forum Ventures 黑客马拉松。经过 10 个多月日常用于构建实际产品后，他将整个工作流开源。结果？一个全面的系统，在 GitHub 上已获得 **17.4 万+ 星标**，超过 **2.8 万次 Fork**。

ECC **不是**一堆配置文件。它是一个完整的、可用于生产的系统：

- **300+ 技能** —— 从代码审查到 TDD 再到深度研究的可复用提示包
- **本能（Instincts）** —— 引导 Claude 默认行为的自动化规则
- **内存优化** —— 面向长期项目的持久化知识图谱
- **持续学习** —— 自动改进循环，不断优化输出质量
- **安全扫描** —— 每次提交前的内置漏洞检测
- **研究优先开发** —— 代码变更前的自动化多源研究
- **MCP 配置** —— 开箱即用的 Model Context Protocol 服务器设置

而且完全 **免费、MIT 协议开源**。

---

## 为什么需要 ECC

如果你用过 Claude Code，你会知道它开箱即用已经很强大了。但当你在实际项目中每天使用时，你会发现：

- 你总是重复输入相同的指令
- 上下文窗口被设置样板填满
- 每次都要重新告诉 Claude 你的项目约定
- 缺少持续改进的机制

ECC 通过提供一个**结构化的增强层**来解决所有这些问题。安装一次，你的 AI 代理就拥有了：

- 一套完整的专业化技能库
- 项目约定和决策的自动记忆
- 内置的安全和代码审查质量门禁
- 写代码之前自动启动的研究能力

---

## 核心功能

### 技能系统

技能是 ECC 的核心工作流界面。它们就像**作用域限定的工作流包**：可复用的提示、结构、支持文件和代码地图，让 Claude 能快速导航你的项目而不消耗上下文。

不需要每次都描述你想要什么，只需敲入斜杠命令：

```
/tdd            → 测试驱动开发工作流
/code-review    → 全面代码审查
/e2e            → 端到端测试设置
/refactor-clean → 死代码清理
/security-review → 安全漏洞扫描
/deep-research  → 多源研究与综合
```

每个技能包括结构化提示、命令处理器和代码地图——Claude 正确执行该工作流所需的一切。

### 本能（Instincts）

"本能"是引导 **Claude 默认如何响应**的自动化行为。ECC 为以下方面配置本能：

- 代码质量标准（不可变性、错误处理、命名规范）
- 项目特定约定（文件组织、测试模式）
- 安全优先开发（输入验证、密钥检测）
- 文档规范（何时以及如何编写文档）

### 内存优化

ECC 实现了**持久化知识图谱**，跨会话跟踪项目实体、决策和关系。这意味着你的 AI 代理会记住：

- 架构决策及其理由
- 哪些模式对你的项目有效
- 关键实体及其关系
- 应指导未来工作的过往决策

不再需要每次会话都重新教导 Claude。

### 持续学习

ECC 包含自动反馈循环，会随着时间推移不断改进输出：

- 运行评估来衡量质量
- 检测过去成功和失败中的模式
- 根据结果优化提示和本能
- 为你的领域构建定制知识库

### 安全扫描

每次提交前，ECC 可以运行安全检查：

- 硬编码密钥和 API 令牌
- SQL 注入漏洞
- XSS 和 CSRF 模式
- 不安全的加密使用
- 依赖漏洞

### 研究优先开发

ECC 推广"先研究再编码"的工作流。当你要求实现一个功能时，它会自动：

1. 搜索现有代码和 GitHub 模式
2. 通过 Context7 查阅库文档
3. 综合发现成果形成计划
4. 然后——也只有到了这个时候——才开始写代码

---

## 跨平台兼容

ECC 的突出特性之一是它 **跨多个 AI 代理平台工作**。你不需要绑定在单一工具上：

| 平台 | 支持 |
|---------|---------|
| **Claude Code** | ✅ 完全支持 |
| **Codex（OpenAI）** | ✅ 完全支持 |
| **Cursor** | ✅ 完全支持 |
| **OpenCode** | ✅ 完全支持 |
| **Gemini** | ✅ 完全支持 |
| **GitHub Copilot** | ✅ 支持 |

一次安装，随处使用。

---

## 项目内容

ECC 包含大量经过生产测试的组件：

- **300+ 技能** 覆盖开发、测试、安全、研究和运维
- **100+ 代理** 用于专业化任务（代码审查、安全、规划、研究）
- **MCP 服务器配置** 用于 Context7、Exa 搜索、数据库、GitHub 等
- **钩子系统** 用于 PostToolUse 格式化、linting 和类型检查
- **语言特定规则** 覆盖 TypeScript、Python、Go、Rust、Swift、PHP 等
- **VSCode 集成** 和编辑器配置
- **插件系统** 实现无缝 Claude Code 集成
- **模板项目** 快速启动

项目跨多种语言——JavaScript（57%）、Rust（33%）、Python（5%）、Shell（3%）、TypeScript（1%）——拥有 170+ 贡献者。

---

## 安装方法

### 方式一：作为插件安装（推荐）

最简单的方式，将 ECC 安装为 Claude Code 插件：

```bash
# 添加市场源
/plugin marketplace add https://github.com/affaan-m/everything-claude-code

# 安装插件
/plugin install ecc@ecc
```

就这样。你现在可以访问所有命令、代理、技能和钩子。

### 方式二：手动安装

克隆仓库并按需复制：

```bash
git clone https://github.com/affaan-m/everything-claude-code.git
cd everything-claude-code

# 复制你的技术栈所需的规则（例如 TypeScript + Web）
cp -r rules/typescript ~/.claude/rules/
cp -r rules/web ~/.claude/rules/
cp -r rules/common ~/.claude/rules/

# 复制你需要的技能
cp -r skills/* ~/.claude/skills/
```

### 方式三：通过 settings.json

直接添加到你的 Claude 配置：

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

## 快速上手

安装完成后，试试这些常用命令：

```
/hookify        → 为项目设置自动化钩子
/init           → 为项目初始化 ECC
/tdd            → 启动测试驱动开发工作流
/code-review    → 审查当前变更
/deep-research  → 实现前进行深度研究
```

或者查看速查指南：`/projects` 查看项目级命令，`/plan` 进入结构化功能规划。

---

## 为什么这很重要

AI 编程代理正在以惊人的速度进步，但模型能力只是方程式的一半。另一半是**你如何引导它**。

ECC 提供了结构、记忆和工作流，将一个 AI 代理从聪明的自动补全转变为可靠、一致的开发伙伴。这就是让 Claude 从"审查一下这段代码"升级为检查安全、风格、测试和架构等 15 个特定质量门禁的差别。

凭借 17.4 万+ 星标和 170+ 贡献者的活跃社区，ECC 已成为增强 AI 编程代理的**事实标准**。它不仅是一个工具——更是一场向正确方向发展的代理式开发运动。

---

**了解更多：**

- GitHub：[github.com/affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code)
- 网站：[ecc.tools](https://ecc.tools)
- 协议：MIT — 自由使用、修改和分享
