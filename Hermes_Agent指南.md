# 全在这了！我把 Hermes Agent 学透后，整理出 80+ 条命令和用法（含教程）

**公众号：AI之志者**
**发布时间：2025年4月12日 02:12**

> ⚠️ **校对说明**：本文依据 [Hermes Agent 官方文档](https://hermes-agent.nousresearch.com/docs) 对原文多处错误进行了修正，修正处已注明。

---

## 安装 / 更新

```bash
# 新用户，一行安装（支持 Linux、macOS、WSL2、Android Termux）
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash

# 安装完善一下 shell
source ~/.bashrc   # zsh 用户换成：source ~/.zshrc

# 老用户，直接更新
hermes update
```

> ⚠️ Windows 原生环境不受支持，请先安装 WSL2，在 Ubuntu 终端里运行上述命令。

---

下面的命令需在终端里运行。

Mac 用户打开「终端」即可，Windows 用户需要先装 WSL2，装好之后打开 Ubuntu 终端运行，文本游戏部分有详细步骤。

Hermes Agent 可接入微信！Github 96K Star，24小时不间断工作。（含教程）

那么，除了和 Hermes 聊天，还能干啥？命令有多少？国内的模型能用哪些？

这篇做到「全都教会你」，整理出来。

---

## 有多少东西

先统一下这篇的信息量。

Hermes 能接入的 AI 模型，国内外加起来超过 20 个，DeepSeek、Kimi、通义千问、智谱 GLM、MiniMax 全都支持，每个怎么配置都有写。

光命令就有 80 多条。顶级的 CLI 命令 30 多个，进入聊天之后还有 50 多条对话指令。

它有个技能图谱，里面 644 个组件，覆盖 Github、写作、研究、机器学习等 16 个方向，一行命令装好。

它不是一个聊天机器人，是 9 个模块组成的完整系统，覆盖对话、自动化、数据处理器、模式对照等等。

整理出 10 条「为什么这样设计」的摘录文（在文末）。

---

## ■ 第一类：启动和会话管理

**你想启动 Hermes，就这个 👇**

```bash
hermes
# 或者
hermes chat
```

**你想继续上次没聊完的对话 👇**

```bash
hermes --continue
# 简写
hermes -c
# 按会话名或 ID 恢复
hermes --resume "会话名或ID"
hermes -r "会话名或ID"
```

> 退出的时候 Hermes 会打印一行恢复命令，下次直接复制粘贴就行。

**你想启动时候选定模型、工具集、档案 👇**

```bash
# 指定模型
hermes chat -m deepseek/deepseek-chat

# 指定工具集
hermes chat -t web,debugging

# 按功能指定（profile）
hermes chat -p github-pr-workflow

# 直接提问，不进入聊天界面
hermes chat -q "帮我写一个 Python 爬虫"

# 安静模式，只输出最终结果
hermes chat -q "今天天气怎么样" --quiet

# 控制最多工具调用次数（默认 10）
hermes chat --max-turns 20

# 开发文件系统的检查点，可以 /rollback 回来
hermes chat --checkpoints
```

**你想管理所有会话，有一整套子命令 👇**

```bash
hermes sessions list              # 列出所有会话
hermes sessions browse            # 交互式浏览
hermes sessions rename ID TITLE   # 重命名
hermes sessions export ID         # 导出会话
hermes sessions delete ID         # 删除某个会话
hermes sessions prune             # 清理老旧会话
hermes sessions stats             # 看统计
```

> 💡 会话内部用 `/title 名字` 可以给当前会话命名；Hermes 的所有对话自动存为本地 SQLite + Markdown 双份，不会丢。

**好用的快捷键 👇**

- `Alt+Enter` 或 `Ctrl+J` → 多行输入换行，粘贴代码时很有用
- 对话中途打新消息并回车 → 中断当前任务并切换到新指令
- `Ctrl+C` → 中断当前操作（2秒内连按两次强制退出）

---

## ■ 第二类：配置和模型切换

**你想换一个模型 👇**

```bash
hermes model
```

会弹出交互式菜单，上下键选，回车确认，10 秒就定。

### 国内可以用的模型

| 提供商 | 支持的模型 | 配置方式 |
|--------|-----------|---------|
| DeepSeek | DeepSeek-V3、R1 等 | 设置 `DEEPSEEK_API_KEY` |
| Kimi / Moonshot | 月之暗面大模型 | 设置 `KIMI_API_KEY` |
| 通义千问 / 阿里云 | Qwen 系列 | 设置 `DASHSCOPE_API_KEY` |
| 智谱 GLM / Z·AI | GLM 系列 | 设置 `ZHIPU_API_KEY` |
| MiniMax（国际端点） | 国际端点 | 设置 `MINIMAX_API_KEY` |
| MiniMax（国内端点） | 国内端点 | 设置 `MINIMAX_CN_API_KEY` |
| 小米 MiMo | MiMo 系列 | 设置对应 API Key |

### 国外提供商也都支持

| 提供商 | 说明 | 配置方式 |
|--------|------|---------|
| Nous Portal | 订阅版，零配置直接用 | `hermes auth` 配置 |
| Anthropic | Claude 系列 | `hermes auth add anthropic --type oauth` |
| OpenAI Codex | GPT 系列 | `hermes auth add openai-codex` |
| OpenRouter | 200+ 模型路由，一个 Key 用多家 | `hermes auth add openrouter --api-key sk-or-xxx` |
| GitHub Copilot | GPT-4.x、Claude 等 | OAuth 认证 |
| Hugging Face | Qwen、DeepSeek 等 20+ 开源模型 | 设置 `HF_TOKEN` |
| NVIDIA NIM | Nemotron 系列 | 设置对应 API Key |

**自己有本地模型（Ollama、vLLM、SGLang 等）👇**

`hermes model` 里选「Custom Endpoint」，填 base URL 和 API Key，上下文窗口大小全都有配置。

**你想查看或改配置 👇**

```bash
hermes config                          # 看当前所有配置
hermes config edit                     # 可视化编辑
hermes config path                     # 看 config.yaml 的位置
hermes config set KEY VAL              # 改某一项
                                       # 例：hermes config set terminal.backend docker
hermes config check                    # 检查写对没有
hermes config migrate                  # 升级配置格式
```

**你想走一道完整的配置向导 👇**

```bash
hermes setup                    # 完整向导（配置所有模块）
hermes setup model              # 只配模型
hermes setup gateway            # 只配消息平台
hermes setup tools              # 只配工具
```

**你想检查环境有没有问题 👇**

```bash
hermes doctor          # 诊断配置和依赖
hermes doctor --fix    # 尝试自动修复
```

**其他常用的 👇**

```bash
hermes status       # 查所有组件状态
hermes version      # 看版本号
hermes update       # 更新到最新版
hermes dump         # 导出完整配置摘要（排查问题时用，适合贴到 Discord/GitHub issue）
```

> ~~`hermes login` / `hermes logout`~~ ✗ **已被移除**（原文有误）
> 请改用 `hermes auth` 系列命令管理凭证。

---

## ■ 密钥管理（Credential Pools）

如果自己有多个 API Key 轮换使用，或者某个 Key 用完了换下一个：

```bash
hermes auth                              # 交互式向导
hermes auth list                         # 查看所有 Key 池
hermes auth list openrouter              # 查看特定提供商
hermes auth add openrouter --api-key sk-or-v1-xxx   # 添加 API Key
hermes auth add anthropic --type oauth   # 添加 OAuth 凭证
hermes auth remove openrouter 2          # 删除（提供商名 + 序号）【原文顺序有误】
hermes auth reset openrouter             # 清除该提供商的冷却时间
```

---

## ■ 插件管理

```bash
hermes plugins          # 交互式管理（General 插件 + Provider 插件综合界面）
hermes plugins list     # 看已装的插件
hermes plugins install  # 安装
hermes plugins remove   # 卸载
```

---

## ■ 外部记忆配置

Hermes 默认记忆存本地。如果想集成 Honcho（用户建模）或 Mem0 等外部服务：

```bash
hermes memory setup       # 配置外部记忆服务
hermes memory status      # 看状态
hermes memory off         # 关闭外部记忆，回到本地
```

---

## ■ MCP 服务管理

MCP（Model Context Protocol）是一个开放协议，让 Hermes 快速接入外部工具服务器，比如 Github、文件系统、数据库等。

```bash
hermes mcp add NAME --url URL         # 添加 HTTP/SSE 类型服务器
hermes mcp add NAME --command CMD     # 添加本地命令行启动的服务器
hermes mcp list                       # 看已配置的服务器
hermes mcp test NAME                  # 测试某服务
hermes mcp configure NAME             # 配置服务器参数
hermes mcp remove NAME                # 删除
hermes mcp serve                      # 把 Hermes 自身作为 MCP 服务器运行
```

**配置文件示例 👇**

```yaml
# ~/.hermes/config.yaml
mcp_servers:
  github:
    command: npx
    args: ["-y", "@modelcontextprotocol/server-github"]
    env:
      GITHUB_PERSONAL_ACCESS_TOKEN: "ghp_xxx"
```

---

## ■ 多实例隔离运行（Profiles）

每个 profile 有独立的 config、记忆、档案、cron，互不干扰：

```bash
hermes profile list              # 看所有 profile
hermes profile create NAME       # 创建 profile
hermes profile use NAME          # 设为默认 profile
hermes profile show NAME         # 查看详情
hermes profile rename A B        # 改名
hermes profile delete NAME       # 删除
hermes profile export NAME       # 导出 tar.gz
hermes profile import FILE       # 从文件导入
```

> 也可以单次指定：`hermes -p 名字` 使用某个 profile 但不改默认设置。

---

## ■ 日志和诊断

```bash
hermes logs                       # 查看日志
hermes dump                       # 导出全量摘要（无 ANSI 颜色，可直接粘贴）
hermes insights                   # 看使用情况
hermes insights --days 7          # 只看最近 7 天
```

---

## ■ Shell 自动补全

```bash
hermes completion bash >> ~/.bashrc    # bash 用户
hermes completion zsh >> ~/.zshrc      # zsh 用户（大多数 Mac）
```

运行完之后重开终端，或执行 `source ~/.bashrc` 立刻生效。

---

## ■ OpenClaw 迁移工具

```bash
hermes claw migrate                   # 交互式迁移（完整预设）
hermes claw migrate --dry-run         # 预览会迁移什么（不实际操作）
hermes claw migrate --preset user-data  # 只迁移数据，不迁移密钥
hermes claw migrate --overwrite       # 覆盖已存在的冲突
```

---

## ■ 卸载

```bash
hermes uninstall
```

---

## ■ 第三类：技能和工具管理

技能（Skills）是一个 Markdown 文件，里面写着「请帮我完成任务，保存个工作框架」。Hermes 会自动读取并作为对话上下文，不用每次重新解释。

**技能还支持条件触发 👇**

```yaml
---
name: deploy-to-vercel
description: 👑 Next.js 部署到 Vercel
platforms: [cli]
conditions: [file:package.json]
---
```

**自己写一个技能 👇**

```bash
mkdir -p ~/.hermes/skills/my-skill/
# 新建 .md 文件，写上 YAML 头和正文
# 然后用 /reload 命令加载，或等 Hermes 自动读取
```

### 技能商店：644 个技能，16 个分类

| 分类 | 代表技能 |
|------|---------|
| AI Agent | claude-code, codex, hermes-agent, opencode |
| Git | github-pr-workflow, github-code-review, codebase-inspection |
| ML Ops | gguf-quantization, whisper, stable-diffusion, unsloth |
| Productivity | ocr, powerpoint, nano-pdf, linear, google-workspace |
| Research | arxiv, llm-wiki, blogswitcher, polymarket |
| Creative | ascii-art, manim-video, excalidraw, songwriting |
| Apple/macOS | apple-notes, apple-reminders, findmy, imessage |
| Media | gif-search, youtube-content |
| Gaming | minecraft-modpack-server, pokemon-player |
| DevOps | webhook-subscriptions |
| Data Science | jupyter-live-kernel |
| Note-taking | obsidian |
| Social Media | zitter |
| Smart Home | openhue |
| MCP | mcporter, native-mcp |
| Software Dev | plan, requesting-code-review, subagent-driven-development |

**技能管理命令 👇**

```bash
hermes skills browse                    # 交互式浏览
hermes skills search 关键词             # 搜索技能
hermes skills search react --source     # 搜索指定注册表
hermes skills install official/security/password  # 安装技能
hermes skills list                      # 看已装的技能
hermes skills inspect ID                # 查详情
hermes skills update                    # 更新已装技能
hermes skills publish                   # 发布自己写的技能
```

**工具管理 👇**

```bash
hermes tools                  # 交互式激活/停用工具
hermes tools list             # 查所有工具
hermes tools enable NAME
hermes tools disable NAME
hermes toolsets               # 看工具集合（分组）
```

---

## ■ 第四类：消息平台和定时任务

Hermes 支持 **15 个以上**的消息平台（原文「16个以上」有误）：

> Telegram、Discord、Slack、WhatsApp、Signal、Matrix、Mattermost、Email、SMS、钉钉（DingTalk）、飞书（Feishu）、企微（WeCom）、BlueBubbles、Home Assistant、CLI

**搭建消息平台 👇**

```bash
hermes gateway setup       # 交互式配置，接入 Telegram、Discord、Slack、WhatsApp、Signal 等
hermes gateway run         # 前台启动
hermes gateway install     # 安装成系统服务
hermes gateway start       # 后台启动
hermes gateway stop        # 停止
hermes gateway restart     # 重启
hermes gateway status      # 看状态
```

**定时任务 👇**

```bash
hermes cron create "9:00"    # 创建定时任务（支持 "9am"、"every 2h"、"0 9 * *"）
hermes cron list             # 查所有
hermes cron edit ID          # 编辑
hermes cron pause ID         # 暂停
hermes cron release ID       # 恢复
hermes cron run ID           # 立刻手动运行一次
hermes cron delete ID        # 删除
hermes cron status           # 查状态
```

**Webhook 👇**

```bash
hermes webhook subscribe 名字     # 订阅 webhook
hermes webhook list
hermes webhook test 名字          # 测试
hermes webhook remove 名字
```

---

## ■ 语音模式

```bash
pip install "hermes-agent[voice]"   # 包含 faster-whisper，本地语音转文字，不用联网
```

进入聊天后：

```bash
/voice on      # 开启语音接入，按 Ctrl+B 录音
/voice off     # 关闭
/voice status  # 看状态
```

> 【原文有误】：开启 `/voice on` 后，按 **`Ctrl+B`** 录音（不是 Ctrl+C）。
> Discord 也支持语音频道，支持多名用户同时说话。

---

## ■ Terminal Backend（终端后端）

Hermes 支持 **6 种** terminal 后端（原文只提了 Docker，有所遗漏）：

| 后端 | 说明 |
|------|------|
| local | 本机直接运行（默认） |
| docker | 容器隔离，保护主机环境 |
| ssh | 远程服务器 |
| daytona | 无服务器持久化（空闲时休眠，近乎零成本） |
| singularity | HPC 环境 |
| modal | 无服务器持久化 |

```bash
hermes config set terminal.backend docker   # 切换到 Docker 后端

# 也可在 config.yaml 里指定镜像
# terminal:
#   backend: docker
#   docker:
#     image: python3.11
#     persistent: true
```

---

## ■ 接入 IDE（ACP 编辑器集成）

Hermes 可作为 VS Code、Zed、JetBrains 的 AI 后端，使用 ACP 协议（Agent Client Protocol）：

```bash
hermes acp    # 启动 ACP stdio 服务器，供编辑器连接
```

> 安装时使用 `.[acp]` extra，或使用 `.[all]` 一次性安装所有功能。

---

## ■ 自定义 Agent 人格（SOUL.md）

文件放在 `~/.hermes/SOUL.md`，每条消息发送前都会重新读取，无需重启：

```
你是一个直接、尽量用文字回答的助手。
你总是聚焦在当前任务上，为用户提供最有效的帮助。
```

> 每个 profile 可以有自己的 SOUL.md，实现多人格隔离。

---

## ■ 第五类：会话内部斜杠指令

进入 Hermes 聊天后，输入 `/` 会自动补全命令。

### 会话控制

| 指令 | 说明 | 频率 |
|------|------|------|
| `/new` | 开个全新的对话 | 高 |
| `/retry` | 重试上一条 | 高 |
| `/undo` | 撤销上一轮对话 | 高 |
| `/compress` | 压缩上下文，省 token | 中 |
| `/rollback` | 回滚到某个文件检查点（需提前开启 `--checkpoints`） | 低 |
| `/title 名字` | 给当前会话命名 | 低 |
| `/save` | 把对话保存成文件 | 低 |
| `/background 任务` | 在后台并行跑一个子 Agent 任务 | 中 |
| `/stop` | 立刻终止当前 Agent 运行 | 中 |

### 配置相关

| 指令 | 说明 | 频率 |
|------|------|------|
| `/model` | 查看和切换当前模型 | 高 |
| `/yolo` | 切换是否跳过危险命令确认 | 中 |
| `/verbose` | 循环切换显示详细程度：off → new → all → verbose | 中 |
| `/settings` | Hermes 设置 | 中 |
| `/loglevel` | 调整日志级别 none/low/medium/high/ultigh | 中 |
| `/personality` | 切换人格风格 | 低 |

### 工具与档案

| 指令 | 说明 | 频率 |
|------|------|------|
| `/tools` | 管理工具 | 中 |
| `/skills` | 搜索安装技能 | 中 |
| `/browser` | 高级 Chrome 浏览器（CDP） | 低 |
| `/cron` | 管理定时任务 | 低 |
| `/mcp` | MCP 服务器管理 | 低 |

### 信息查看

| 指令 | 说明 | 频率 |
|------|------|------|
| `/usage` | 看 token 用了多少 | 高 |
| `/quit` / `/exit` / `/q` | 退出 | - |

### Telegram / Discord 专属指令

| 指令 | 说明 |
|------|------|
| `/diary` | 记笔记 |
| `/tasks` | 任务管理 |
| `/update` | 在平台里更新 Hermes |

---

## ■ 奇技 + 组合用法

**Windows 用户请先安装 WSL2**

```bash
wsl --install    # PowerShell 里执行，重启后打开 Ubuntu 终端
```

**`/rollback` 要先开启**

```bash
hermes chat --checkpoints    # 开启检查点，之后才能 /rollback 回滚
```

**`/yolo` 用之前要清楚**

这个命令会跳过所有操作的确认提示（跑脚本、跑 SQL、执行命令等），调试方便，但别忘了关。

**几个实际的绝妙组合 👇**

```bash
# 直接提问 + 指定模型，不进入聊天界面
hermes chat -q "帮我写一个 Python 爬虫" -m deepseek/deepseek-chat

# 继续上次工作 + 指定工作流
hermes chat --continue -p github-pr-workflow

# 安静模式，只输出最终结果
hermes chat -q "今天天气怎么样" --quiet
```

`hermes gateway run` 搭上 cron 任务，整一套自动定时对话发送通知。

---

## ■ 嵌在脚本/应用里重用 Hermes

```bash
pip install git+https://github.com/NousResearch/hermes-agent.git
```

```python
from rns_agent import AiAgent

agent = AiAgent()
result = agent.run_conversation("我需要办理什么？")
print(result)
```

---

## ■ 10 条设计洞见

超读 Hermes 的源码之后，整理出 10 条对其复杂设计决策的思考：

1. **持续摘要取代整理大模型上下文** — 把「日次」摘要放在每次对话开始，约占 AI 处理时间的 80%。

2. **每个 Agent 是同步的，没有 async agents** — 「一件事完成再下一件」的方式，控速更稳，代码更容易维护。

3. **工具是本地读出的，不需要中心配置文件** — 加一个新工具，只需写好工具本身，框架自动发现。

4. **技能是基础文本文件，不是代码** — 可以用记事本打开，Hermes 自己读取，这才是真正的「自学习」。

5. **记忆的目标是「减少未来的纠正」** — 不是完整记录所有数据，而是应对「下次怎么处理更好」的约定。

6. **高全活动最范用的是 FTS5 全文检索型 LLM 搜索** — 让你总能翻到跨会话的相关记录，不再重复提问。

7. **子 Agent 有工具限制和数量上限** — 每个小助手最多并发 3 个，超过失效，防止失控。

8. **Gateway 最多 300 秒活动自动发回记忆** — 在 Telegram 里 5 分钟记够，它会自动把内容回写存档。

9. **MCP 客户端实现约 2195 行** — 接外部工具功能复杂，高度符合标准规范。

10. **每次文件活动都触发 git commit** — 每次改文件前先写基准，改完了 `/rollback` 可以一步步撤回来，设计灵感来自 Claude Code。

---

想要一起长期探索 Hermes 的完整 AI Agent 工具社区的朋友，可以在公众号后台私发「Agent」进群交流。

---

## 参考来源

- [Hermes Agent 官方文档](https://hermes-agent.nousresearch.com/docs)
- [Hermes Agent CLI 命令参考](https://hermes-agent.nousresearch.com/docs/reference/cli-commands)
- [Hermes Agent 官方 Github](https://github.com/NousResearch/hermes-agent)

`#HermesAgent` `#Agent` `#AI之志者` `#OpenClaw` `#AIAgent`

---

*公众号：AI之志者 | AI测评家，专注人工智能 AI…… | 140多篇结构文章*
