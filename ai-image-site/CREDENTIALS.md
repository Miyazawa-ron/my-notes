# SKY AI 平台 — 重要信息备忘

> ⚠️ 此文件包含敏感信息，请勿分享给他人

---

## 🌐 网站信息

| 项目 | 内容 |
|------|------|
| 正式地址 | https://skylife-sakura.com |
| 备用地址 | https://skylife-image.skylife-sakura.workers.dev |
| 管理后台 | 登录后点右上角「管理后台」按钮 |

---

## 👤 管理员账号

| 项目 | 内容 |
|------|------|
| 邮箱 | admin@skylife.com |
| 密码 | admin123（上线前请修改！） |
| 余额 | 99999 积分 |

---

## ☁️ Cloudflare

| 项目 | 内容 |
|------|------|
| Worker 名称 | skylife-image |
| D1 数据库 | skylife-db |
| 数据库 ID | 7ea7c759-1364-4c42-ae48-8f5b79dbdeed |
| workers.dev 子域名 | skylife-sakura |
| 自定义域名 | skylife-sakura.com |

---

## 🤖 AI API

| 服务 | 说明 |
|------|------|
| OpenAI | 账号：b6v58c@bma.biglobe.ne.jp，余额 $10，Organization：SKYライフ |
| 火山引擎 Seedance | API Key 已配置到 Cloudflare Secrets |
| Secrets 名称 | OPENAI_API_KEY / VOLCENGINE_API_KEY |

---

## 💰 积分计费

| 模型 | 消耗 |
|------|------|
| GPT Image | 10 积分/张 |
| Seedance | 20 积分/次 |

---

## 🛠️ 本地开发环境

| 项目 | 内容 |
|------|------|
| 项目目录 | ~/hermes-webui/skylife-image |
| 部署命令 | cd ~/hermes-webui/skylife-image && npx wrangler deploy |
| 查看日志 | npx wrangler tail |
| 本地测试 | npx wrangler dev |

---

## 📋 常用管理命令

```bash
# 进入项目目录
cd ~/hermes-webui/skylife-image

# 部署更新
npx wrangler deploy

# 查询用户余额
npx wrangler d1 execute skylife-db --remote --command="SELECT email, balance FROM users;"

# 手动充值（替换邮箱和积分数）
npx wrangler d1 execute skylife-db --remote --command="UPDATE users SET balance = balance + 100 WHERE email='user@example.com';"

# 查看生成记录
npx wrangler d1 execute skylife-db --remote --command="SELECT * FROM generations ORDER BY created_at DESC LIMIT 10;"
```

---

## ⚠️ 待办事项

- [ ] 上线前修改管理员密码 admin123
- [ ] Seedance 视频生成超时问题（需升级 Workers Paid $5/月 或改为异步架构）
- [ ] 用量增大后接入聚合免签支付

---

最后更新：2026-05-06
