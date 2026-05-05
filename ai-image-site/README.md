# AI图片生成中转站 — 搭建任务清单

> 目标：为国内朋友搭建自助AI图片生成网站
> 域名：skylife-sakura.com（Cloudflare 托管）

---

## 需求确认（已定）

| 项目 | 决定 |
|------|------|
| 用户登录 | 邮箱注册 + 登录账号系统 |
| 计费方式 | 充值余额，按用量扣费 |
| 支持模型 | GPT Image + Seedance 双模型 |
| 界面语言 | 中文 |
| 支付方式 | 个人收款码 + 手动充值（起步阶段） |

---

## 技术栈（已定）

| 层级 | 技术 | 原因 |
|------|------|------|
| 前端 | HTML + CSS + JS（单页） | 轻量，无需框架 |
| 后端 | Cloudflare Workers | 无服务器，域名已在CF |
| 数据库 | Cloudflare D1（SQLite） | 免费，够用 |
| 部署 | Cloudflare Pages + Workers | 一体化，免费套餐足够 |

---

## 第一阶段：账号与环境准备

- [x] OpenAI 账号 — 已有并充值
- [x] 火山引擎账号 — 已注册
- [x] 域名 skylife-sakura.com — Cloudflare 已注册
- [ ] 火山引擎 — 控制台开通 Seedance API，复制 API Key
- [ ] OpenAI — 复制 API Key 备用

---

## 第二阶段：技术环境准备

- [ ] 安装 Node.js（Windows PC）— https://nodejs.org 下载LTS版
- [ ] 安装 Wrangler CLI（Cloudflare 开发工具）
      npm install -g wrangler
- [ ] Wrangler 登录 Cloudflare 账号
      wrangler login
- [x] VS Code 已有
- [x] GitHub 账号 miyazawa-ron 已有

---

## 第三阶段：搭建顺序

### Step 1 — 创建 Cloudflare D1 数据库
- [ ] 建库：wrangler d1 create image-site-db
- [ ] 建表：users（用户）、transactions（充值记录）、generations（生图记录）

### Step 2 — 搭后端 Worker
- [ ] 用户注册 / 登录 / Token 验证接口
- [ ] 余额查询 / 管理员充值接口
- [ ] GPT Image 生图接口
- [ ] Seedance 生图接口

### Step 3 — 搭前端页面
- [ ] 注册 / 登录页
- [ ] 主界面（提示词输入 + 模型选择 + 生成按钮）
- [ ] 图片展示区 + 历史记录
- [ ] 余额显示
- [ ] 管理员充值页（简单密码保护）

### Step 4 — 部署上线
- [ ] 部署 Worker 到 Cloudflare
- [ ] 绑定 skylife-sakura.com 域名
- [ ] 全流程测试

---

## API 资源汇总

| 服务 | 状态 | 备注 |
|------|------|------|
| OpenAI（GPT Image） | 已有 | 日本网络直连 |
| 火山引擎（Seedance） | 已注册 | 待获取 API Key |
| 域名 skylife-sakura.com | 已注册 | Cloudflare 托管 |
| Cloudflare Workers/D1 | 待开通 | 免费套餐足够 |

---

## 支付方案

| 阶段 | 方案 |
|------|------|
| 起步 | 个人收款码 + 手动充值（管理员后台加余额） |
| 扩大 | 聚合免签支付（码支付/Epay，自动回调） |

---

最后更新：2026-05-05（需求已确认，进入搭建阶段）
