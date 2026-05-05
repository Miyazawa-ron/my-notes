# AI图片生成中转站 — 搭建任务清单

> 目标：为国内朋友搭建自助AI图片生成网站，支持 GPT Image / Seedance，手动充值余额管理。
> 域名：skylife-sakura.com（Cloudflare 托管）

---

## 第一阶段：账号与环境准备

- [x] OpenAI 账号 — 已有并充值
- [x] 火山引擎账号 — 已注册（Seedance API）
- [x] 域名 — skylife-sakura.com（Cloudflare 已注册）
- [ ] 火山引擎 — 申请 Seedance API 权限，获取 API Key
- [ ] 服务器 — 选择方案（Cloudflare Workers 或 VPS）

---

## 第二阶段：技术环境准备

- [ ] 本地安装 Node.js — 在 Windows PC 上装好
- [ ] 代码编辑器 — VS Code（已有）
- [x] GitHub 账号 — miyazawa-ron，已有

---

## 第三阶段：确认需求细节

- [ ] 用户登录方式 — 注册/登录系统 or 专属密码？
- [ ] 计费单位 — 按次收费 or 充值余额扣费？
- [ ] 支持模型 — 仅 GPT Image or 同时支持 Seedance？
- [ ] 界面语言 — 中文？

---

## 第四阶段：搭建（逐步实现）

- [ ] 搭后端 API 服务（提示词 → 调用图片API → 返回结果）
- [ ] 搭前端页面（提示词输入、模型选择、图片展示）
- [ ] 用户余额系统（手动充值后台）
- [ ] 部署上线（绑定 skylife-sakura.com）
- [ ] 测试全流程

---

## 支付方案

| 阶段 | 方案 |
|------|------|
| 起步 | 个人收款码 + 手动充值 |
| 扩大 | 聚合免签支付（码支付/Epay） |

---

## API 资源汇总

| 服务 | 状态 | 备注 |
|------|------|------|
| OpenAI（GPT Image） | 已有 | 日本网络直连 |
| 火山引擎（Seedance） | 已注册 | 待获取 API Key |
| 域名 skylife-sakura.com | 已注册 | Cloudflare 托管 |

---

最后更新：2026-05-05
