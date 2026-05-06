# AI图片生成中转站 — 搭建任务清单

> 目标：为国内朋友搭建自助AI图片生成网站
> 网站地址：https://skylife-image.skylife-sakura.workers.dev
> 域名：skylife-sakura.com（Cloudflare 托管，待绑定）

---

## 需求确认（已定）

| 项目 | 决定 |
|------|------|
| 用户登录 | 邮箱注册 + 登录账号系统 |
| 计费方式 | 充值余额，按用量扣费 |
| 支持模型 | GPT Image（10积分/张）+ Seedance（20积分/次） |
| 界面语言 | 中文 |
| 支付方式 | 个人收款码 + 手动充值（起步阶段） |

---

## 技术栈（已定）

| 层级 | 技术 |
|------|------|
| 前端 | HTML + CSS + JS（单页） |
| 后端 | Cloudflare Workers |
| 数据库 | Cloudflare D1（SQLite） |
| 部署 | Cloudflare Workers + Assets |

---

## 第一阶段：账号与环境准备

- [x] OpenAI 账号 — 已有并充值（$10）
- [x] 火山引擎账号 — 已注册，API Key 已配置
- [x] 域名 skylife-sakura.com — Cloudflare 已注册
- [x] OpenAI API Key — 已配置到 Cloudflare Secrets
- [x] 火山引擎 API Key — 已配置到 Cloudflare Secrets

---

## 第二阶段：技术环境准备

- [x] Node.js v22.22.2 — Mac 已安装
- [x] Wrangler 4.87.0 — 已安装并登录
- [x] VS Code — 已有
- [x] GitHub 账号 miyazawa-ron — 已有

---

## 第三阶段：搭建（已完成）

- [x] 创建 Cloudflare D1 数据库 skylife-db（APAC区域）
- [x] 建表：users / transactions / generations
- [x] 后端 Worker（src/index.js）— 所有API接口完成
- [x] 前端页面（public/index.html）— 中文界面完成
- [x] 部署上线 — 已部署到 workers.dev

---

## 第四阶段：测试结果

- [x] 用户注册/登录 — 正常
- [x] 管理员后台 — 正常（充值/用户列表）
- [x] GPT Image 生图 — 成功！（日式庭院水墨风格测试通过）
- [ ] Seedance 视频生成 — 待测试
- [ ] 绑定自定义域名 skylife-sakura.com

---

## API 接口列表

| 接口 | 功能 |
|------|------|
| POST /api/register | 用户注册 |
| POST /api/login | 用户登录 |
| GET /api/me | 查看余额 |
| POST /api/generate/gpt | GPT Image 生图（扣10积分） |
| POST /api/generate/seedance | Seedance 生成（扣20积分） |
| GET /api/history | 历史记录 |
| POST /api/admin/topup | 管理员充值 |
| GET /api/admin/users | 管理员查看用户 |

---

## 支付方案

| 阶段 | 方案 |
|------|------|
| 起步（当前） | 个人收款码 + 管理员手动充值积分 |
| 扩大 | 聚合免签支付（码支付/Epay，自动回调） |

---

## 后续待办

- [ ] 绑定 skylife-sakura.com 域名
- [ ] 测试 Seedance 视频生成
- [ ] 给朋友开通账号并充值积分
- [ ] 考虑升级自动支付（用量增大后）

---

最后更新：2026-05-06（GPT Image 生图测试成功，平台正式上线！）
