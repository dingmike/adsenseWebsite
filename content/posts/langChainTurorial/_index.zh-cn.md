---
title: "LangChain 入门实战：手把手教你用 20 行代码搭建第一个 AI 应用"
weight: 1
draft: false
description: "LangChain 入门实战：手把手教你用 20 行代码搭建第一个 AI 应用"
tags: ["AI", "Agent", "langChain" ]
---

![Everything Claude Code](featured.png "LangChain")
-----

## 你是不是也写过这样的代码？

你有没有试过，自己写代码去调用大模型的接口？

我猜很多人第一次都是这么过来的：先把 prompt 用 f-string 拼出来，再发一个 HTTP 请求，拿到返回后翻半天找 `content` 字段，最后还要处理超时、报错、重试……

麻烦吗？挺麻烦的。

更麻烦的是：今天用的 OpenAI，明天想换成 DeepSeek，或者加个记忆功能，代码基本要推倒重写。

那有没有一个框架，能把"调模型"这件事做得又快又优雅？

有。它就是 **LangChain**。

今天这篇文章，我不打算讲太多枯燥的理论。我会直接带你写一个能跑起来的小项目，让你 20 分钟内，用 20 行代码，搭出你的第一个 AI 应用。

## LangChain 是什么？

先用一个类比帮大家建立感觉。

你可以把大模型（GPT、DeepSeek、通义千问）想象成一台**发动机**。发动机马力很大，但它只是一个零件，不会自己跑。

而 LangChain 就是那辆**车架**：它把方向盘、仪表盘、变速器都给你装好了，你要做的，只是把发动机放进去。

用官方的话说，LangChain 是一个**大模型应用开发框架**。它帮你把 AI 应用里那些"每次都差不多"的活——管理提示词、调用模型、解析结果、保存记忆、接工具、查文档——全部打包成标准零件。

这些零件，可以用一根"管道"串起来。

## 三个核心概念，一分钟搞懂

LangChain 的零件很多，但新手只需要记住三个：

**① 模型（Model）**：负责"思考"。比如 `ChatOpenAI`，我们通过它调用 GPT、DeepSeek 等大模型。

**② 提示词模板（Prompt Template）**：负责"组织提问方式"。你只要挖好空，把参数填进去，它自动生成规范的问题。

**③ 输出解析器（Output Parser）**：负责"整理回答"。把模型返回的复杂结果，变成干净的纯文本或 JSON。

这三个零件，用管道符 `|` 串起来，就成了一条"链"（Chain）：

```
prompt | llm | parser
```

是不是很像 Linux 的管道命令？这就是 LangChain 的核心思想——**一切皆可串联**。

理论到此为止，下面直接上代码。

## 实战：20 行代码搭建一个 AI 问答助手

我们做一个很实用的例子：**AI 问答助手**。你告诉它一个角色，再抛给它一个问题，它用这个角色的口吻来回答。

比如让它扮演"健身教练"，回答"连续加班很疲惫怎么恢复"，或者扮演"语文老师"，给孩子讲一道阅读理解题。

### 第 1 步：安装

打开终端，运行：

```bash
pip install langchain langchain-openai python-dotenv
```

装三个包就够：`langchain` 是核心框架，`langchain-openai` 负责对接大模型，`python-dotenv` 用来读取密钥配置。

### 第 2 步：配置密钥

在项目文件夹里新建一个文件，命名为 `.env`，填入你的 API 密钥：

```bash
OPENAI_API_KEY=sk-你的密钥
```

> 💡 **国内用户看这里**：如果没有 OpenAI 的 key，可以用 DeepSeek 等国产模型，也是 OpenAI 兼容的接口，代码几乎不用改。方式见文末。

### 第 3 步：写代码

新建 `main.py`，把下面这段代码复制进去：

```python
import os
from dotenv import load_dotenv
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# 加载 .env 里的密钥
load_dotenv()

# ① 模型：负责"思考"
llm = ChatOpenAI(model="gpt-4o-mini", temperature=0.7)

# ② 提示词模板：负责"组织提问方式"，{role} 和 {question} 是留的空
prompt = ChatPromptTemplate.from_template(
    "你是一位{role}。请用简洁、通俗的语言回答下面的问题，控制在100字以内。\n\n问题：{question}"
)

# ③ 输出解析器：负责"把回答整理成干净的文本"
parser = StrOutputParser()

# ④ 用 | 管道把三个组件串成一条"链"
chain = prompt | llm | parser

# ⑤ 运行这条链
result = chain.invoke({
    "role": "资深健身教练",
    "question": "我连续加班一个月，特别疲惫，在家如何快速恢复精力？"
})
print(result)
```

对，核心逻辑就这 20 行左右。

### 第 4 步：运行

```bash
python main.py
```

正常情况下，你会看到类似这样的输出：

> 先别硬扛！建议这样调整：①每天保证7小时睡眠，哪怕分段睡；②工作间隙做5分钟深呼吸或拉伸；③睡前远离手机，喝点温水；④周末安排一次30分钟快走，不要剧烈运动。恢复是马拉松，不是冲刺。

换个角色、换个问题，再跑一次：

```python
result = chain.invoke({
    "role": "小学语文老师",
    "question": "怎么帮三年级孩子提高阅读理解能力？"
})
```

你会发现，**代码一行都不用改**，只是换了个参数，AI 就换了个"人设"。

这就是模板 + 链的威力。

## 如果不用 LangChain，代码会变成什么样？

没有对比，你感受不到它的价值。

同样一个功能，不用 LangChain 大概要写这么多：手动拼 prompt、发 HTTP 请求、解析 JSON、处理各种异常……

每个步骤都要自己写，代码量翻两三倍不说，一旦换模型、加参数，又得重写。

而用 LangChain，核心就是一行管道：

```python
chain = prompt | llm | parser
```

逻辑清清楚楚，改起来也简单——想换模型，改一行；想加记忆，链子上再挂一个零件。

这就是框架存在的意义：**把重复的活替你干了，让你只关注业务本身。**

## 从一个助手，到真正的 AI 应用

上面的例子只是起点。LangChain 真正强大的地方，是它丰富的零件库。当你的需求变复杂时，只要往链子上"挂"更多零件：

**加记忆（Memory）**：让 AI 记得你们之前聊过什么，多轮对话不再是"失忆患者"。

**加工具（Tools）**：让 AI 会查天气、查时间、算数、调用你自己的函数，从一个"聊天机器"变成能干活的"智能体"。

**加检索（RAG）**：把你的文档、PDF、数据库喂给 AI，让它基于你的资料回答，做"专属知识库问答"。

**加编排（LangGraph）**：当流程太复杂时，用 LangGraph 把步骤组织成一张图，让 AI 自己决定走哪条分支。

进阶路径也很清晰：**先跑通基础链 → 做多轮对话 → 接工具 → 做文档问答**。每走一步，能力都上一个台阶。

## 为什么推荐它？

最后说说，为什么是 LangChain，而不是自己造轮子。

**第一，模型随便换。** 接口统一，今天 GPT、明天 DeepSeek、后天通义千问，改一行配置就行，业务代码零改动。在模型快速迭代的当下，这一点太重要了。

**第二，组件可复用。** prompt、解析器、记忆、检索，都是标准零件，写一次到处用，还能跟社区分享。

**第三，生态成熟。** 官方有配套的 LangSmith（调试追踪）、LangGraph（流程编排）、LangServe（快速部署），从开发到上线，一条龙。

**当然，它也有"缺点"。** 版本更新很快，名词概念多，网上很多老教程还停留在旧 API。建议学的时候**直接看官方最新文档**，代码以能跑通为准。

## 新手最容易踩的 3 个坑

第一次玩 LangChain，这几个坑几乎人人都会遇到，提前帮你排掉：

**① 密钥别写死在代码里。** 用 `.env` 文件加 `load_dotenv()` 加载，既安全，换环境也方便。请一定记住：密钥千万不要提交到 GitHub，不然会被爬虫扫走。

**② 版本不同，API 会变。** LangChain 迭代很快，网上很多老教程还在用已经废弃的 `LLMChain` 写法。你照着抄却报错，大概率不是你的问题，而是版本变了。最靠谱的方法是直接查官方文档；也可以锁定版本安装，比如 `pip install langchain==0.3.*`，避免某天升级把项目搞坏。

**③ 提示词比模型更能决定效果。** 同一个模型，你把角色、格式要求写清楚，输出质量立刻不一样。模板里的 `{role}`、`{question}` 就是两只调节旋钮，多试几次、多调几轮，往往比花钱换更大的模型划算得多。

## 总结

回顾一下今天的内容：

- LangChain 是大模型应用开发框架，帮我们省去重复的"搬砖"代码。
- 核心就三个零件：**模型 + 提示词模板 + 输出解析器**，用 `|` 管道串成链。
- 一个 20 行的 `chain = prompt | llm | parser`，就能搭出你的第一个 AI 应用。

如果你能跑通今天这个例子，恭喜你，已经迈出大模型应用开发的第一步了。

下一步，试着给它加上记忆，做一个真正能陪你聊天的 AI 助手吧。要是想继续看，我下一篇就写"LangChain 记忆功能实战"。

有任何问题，欢迎在评论区留言交流。

> 💡 补充：国内用户可以使用 DeepSeek，只需把第 3 步中的 `llm` 换成：
>
> ```python
> llm = ChatOpenAI(
>     model="deepseek-chat",
>     api_key=os.getenv("DEEPSEEK_API_KEY"),
>     base_url="https://api.deepseek.com/v1",
> )
> ```
>
> 然后在 `.env` 里填入 `DEEPSEEK_API_KEY=你的密钥` 即可。

**官方文档**：https://python.langchain.com/
