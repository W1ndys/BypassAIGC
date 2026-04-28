# 用户指令记忆

本文件记录了用户的指令、偏好和教导，用于在未来的交互中提供参考。

## 格式

### 用户指令条目
用户指令条目应遵循以下格式：

[用户指令摘要]
- Date: [YYYY-MM-DD]
- Context: [提及的场景或时间]
- Instructions:
  - [用户教导或指示的内容，逐行描述]

### 项目知识条目
Agent 在任务执行过程中发现的条目应遵循以下格式：

[项目知识摘要]
- Date: [YYYY-MM-DD]
- Context: Agent 在执行 [具体任务描述] 时发现
- Category: [代码结构|代码模式|代码生成|构建方法|测试方法|依赖关系|环境配置]
- Instructions:
  - [具体的知识点，逐行描述]

## 去重策略
- 添加新条目前，检查是否存在相似或相同的指令
- 若发现重复，跳过新条目或与已有条目合并
- 合并时，更新上下文或日期信息
- 这有助于避免冗余条目，保持记忆文件整洁

## 条目

### 项目技术栈与结构
- Date: 2026-04-28
- Context: Agent 在执行"任务排队运行"功能改造时发现
- Category: 代码结构
- Instructions:
  - 前端: React + Vite，位于 `package/frontend/`
  - 后端: Python FastAPI，位于 `package/backend/`
  - 前端页面: `WorkspacePage.jsx`（论文优化）和 `WordFormatterPage.jsx`（Word 排版）
  - 后端并发管理: `app/services/concurrency.py` 中的 `ConcurrencyManager` 已支持任务队列
  - API 层: `app/routes/optimization.py`（优化路由）和 `app/routes/word_formatter.py`（Word 排版路由）
  - 前端 API 封装: `src/services/api.js`

### 任务并发模型
- Date: 2026-04-28
- Context: Agent 在执行"任务排队运行"功能改造时发现
- Category: 代码模式
- Instructions:
  - 后端 `ConcurrencyManager` 已有队列机制，支持多任务排队执行
  - 前端原先使用单一 `activeSession`/`activeJob` 状态，限制了只能同时追踪一个任务
  - 已改为 `activeSessions`/`activeJobs`（Set 类型）支持多任务并行追踪
  - WorkspacePage 使用轮询（4秒间隔）获取进度
  - WordFormatterPage 使用 SSE（Server-Sent Events）获取实时进度

### 构建方法
- Date: 2026-04-28
- Context: Agent 在执行前端构建验证时发现
- Category: 构建方法
- Instructions:
  - 前端构建: `cd package/frontend && npx vite build`
  - 需要先 `npm install` 安装依赖
