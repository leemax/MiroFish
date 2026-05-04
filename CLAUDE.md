# MiroFish - Claude Code 项目指导

## 项目简介

MiroFish 是基于多智能体技术的 AI 预测引擎，从现实种子信息构建平行数字世界并演化推演。详细介绍见 `README.md`。

- **后端**：Python（≥3.11，≤3.12）+ FastAPI，使用 `uv` 管理依赖，位于 `backend/`
- **前端**：Node.js（≥18）+ Vite + React，位于 `frontend/`
- **根目录**：npm monorepo，统一编排前后端启动

## 常用命令

```bash
npm run setup:all     # 一键安装根/前端/后端依赖
npm run dev           # 同时启动前后端（前 :3000，后 :5001）
npm run backend       # 仅启动后端：cd backend && uv run python run.py
npm run frontend      # 仅启动前端：cd frontend && npm run dev
npm run build         # 构建前端生产产物
```

后端单独操作时一律使用 `uv`，**不要混用 pip**：

```bash
cd backend && uv sync       # 同步依赖
cd backend && uv run <cmd>  # 在虚拟环境中执行命令
```

## 环境变量

复制 `.env.example` 到 `.env`，填入：

- `LLM_API_KEY` / `LLM_BASE_URL` / `LLM_MODEL_NAME`（OpenAI 兼容 LLM）
- `ZEP_API_KEY`（Zep Cloud）

**绝不提交 `.env` 或任何含密钥的文件**。`.gitignore` 已覆盖。

## 目录约定

| 目录 | 内容 |
|---|---|
| `backend/` | Python 后端（FastAPI、Agent 逻辑、数据模型） |
| `backend/uploads/` | 用户上传文件（已 gitignore） |
| `backend/logs/` | 运行日志（已 gitignore） |
| `frontend/` | Vite + React 前端 |
| `static/` | README/文档使用的静态资源 |
| `.github/workflows/` | CI 配置 |
| `data/` | Docker 数据卷（已 gitignore） |

## 编码规范

- 保持现有项目风格，不要顺手做与任务无关的重构
- 后端遵循 PEP 8；前端遵循 ESLint
- 修改前先阅读相关文件，避免破坏既有约定
- 写注释只解释 WHY，不解释 WHAT

## 跨设备工作流

新设备首次配置：

```bash
git clone https://github.com/leemax/mirofish.git
cd mirofish
cp .env.example .env       # 填入个人密钥
npm run setup:all
claude                     # 启动 Claude Code CLI
```

日常同步：`git pull` → 编码 → `git push`。`.claude/settings.json` 与本文件随仓库同步。

## Claude Code 网页版

仓库已为 claude.ai/code 准备好：网页版会自动加载本文件和 `.claude/settings.json`。
仓库所有者需在 https://github.com/apps/claude 安装 Claude GitHub App，授予 `leemax/mirofish` 权限。

## 个人本地覆盖

不希望共享的配置放 `.claude/settings.local.json`（已 gitignore），不要修改 `.claude/settings.json` 用作个人定制。
