# 办公流程自动化 Agent — Planner 文档

## 1. 项目目标（一句话总结）

构建一套基于 LangGraph 多 Agent 架构的企业级办公流程自动化系统，为跨境电商企业实现运营流程自动化、竞品定价监测、活动/广告自动化配置和日报自动生成，将重复性人工操作减少 80% 以上。

## 2. 需求拆解（P0 / P1 / P2 核心功能模块）

### P0 — MVP 核心（必须上线）

| 模块 | 说明 |
|------|------|
| **多 Agent 编排引擎** | LangGraph 主图 + 子图架构，支持意图路由、状态管理、容错重试 |
| **竞品定价监测 Agent** | 定时爬取竞品网站婚纱价格，结构化存储，价格变动告警 |
| **日报自动生成 Agent** | 聚合运营数据、销售数据、竞品数据，生成长文日报（支持 Markdown/PDF） |
| **运营任务调度 Agent** | 基于 cron 表达式的定时任务管理，触发各 Agent 执行 |
| **意图检测模块** | LLM 驱动的自然语言意图分类，将用户指令路由到对应子 Agent |
| **Web Dashboard（基础版）** | 可视化查看运行状态、日报预览、价格监测结果 |

### P1 — 延后但重要

| 模块 | 说明 |
|------|------|
| **活动/广告自动化配置 Agent** | 自动创建/修改平台促销活动、广告组（Shopify/Google Ads API） |
| **异常检测与告警 Agent** | 基于历史数据的异常值检测（销量突降、价格异常），多渠道推送 |
| **数据看板（增强版）** | 交互式图表、历史趋势分析、导出报表 |
| **多平台数据桥接** | 对接企业的 ERP/OMS/CRM 系统，双向数据同步 |

### P2 — 远期规划

| 模块 | 说明 |
|------|------|
| **AI 决策建议 Agent** | 基于市场数据和历史策略，给出定价/广告出价建议 |
| **多语言翻译 Agent** | 自动化商品描述、营销文案的多语言生成与翻译 |
| **供应链协同 Agent** | 监测库存水位，自动触发采购/补货流程 |
| **用户行为分析 Agent** | 站内用户行为追踪，生成用户分群和转化漏斗分析 |

### 明确不做什么

- 不自己做电商平台（Shopify 已有）
- 不自己做 CRM/ERP（对接已有系统）
- 不做移动端 App（Web 优先，后续可 API 输出到飞书/钉钉）
- 不做实时聊天客服（那是独立系统）

## 3. 技术选型

### 前端
| 技术 | 选择 | 理由 |
|------|------|------|
| 框架 | **React 18 + TypeScript** | 生态成熟、组件库丰富、招聘市场通用 |
| 状态管理 | **Zustand** | 轻量、无样板代码、TS 友好 |
| UI 组件 | **Ant Design** | 企业级 UI 组件库，表格/表单/图表开箱即用 |
| 图表 | **Recharts / ECharts** | 可视化看板需求，ECharts 更强大 |
| 构建 | **Vite** | HMR 快，开发体验好 |
| 网络请求 | **React Query (TanStack Query)** | 请求缓存、自动重试、状态管理 |

### 后端
| 技术 | 选择 | 理由 |
|------|------|------|
| 语言/框架 | **Python 3.11+ / FastAPI** | AI 生态最佳语言，异步支持好，性能高 |
| Agent 框架 | **LangGraph** | 多 Agent 编排、状态图、子图支持 |
| 任务调度 | **APScheduler + Celery** | 定时任务 + 异步任务队列 |
| LLM 接口 | **OpenAI API / Claude API** | 意图检测、日报生成、决策建议 |
| 爬虫 | **Playwright + BeautifulSoup** | 竞品网站数据采集，支持 JS 渲染 |
| 数据验证 | **Pydantic v2** | 与 FastAPI/LangGraph 深度集成 |
| WebSocket | **FastAPI WebSocket** | 实时推送运行状态和告警 |

### 数据库
| 技术 | 选择 | 理由 |
|------|------|------|
| 主数据库 | **PostgreSQL 15+** | 结构化数据存储，JSONB 支持半结构化数据 |
| 缓存 | **Redis** | 任务队列、缓存、Session 管理 |
| 向量数据库 | **pgvector (PostgreSQL 插件)** | 未来 RAG 检索场景，避免引入额外组件 |
| 时间序列 | **TimescaleDB (PostgreSQL 扩展)** | 监控指标、价格历史趋势存储 |

### 部署方式
| 技术 | 选择 |
|------|------|
| 容器化 | **Docker + Docker Compose** |
| 容器编排 | **Kubernetes（生产）/ Docker Compose（开发）** |
| 云服务 | **AWS（ECS / EKS / RDS / ElastiCache）** |
| 反向代理 | **Nginx + Let's Encrypt** |
| 监控 | **Prometheus + Grafana** |

## 4. AI/RAG 判断

### 需要多 Agent 架构
- **原因**：办公自动化涉及多个独立但有交互的专业领域（爬虫、数据分析、文案生成、任务调度），单一 Agent 难以管理状态和上下文。LangGraph 的主图+子图模式天然适合：
  - 主图：意图检测 -> 路由到子 Agent -> 聚合结果
  - 子图：每个 Agent 内部可能有自己的小工作流（如爬虫 Agent：解析 URL -> 渲染页面 -> 提取结构化数据 -> 写入数据库）

### 不需要 LoRA 微调
- **原因**：
  - 所有任务（意图分类、日报生成、数据分析）均可通过 Prompt Engineering + Few-shot 完成
  - LoRA 微调的维护成本高，且数据量不足以训练出稳定模型
  - 调用闭源 API（GPT-4 / Claude）的效果已经足够

### 暂不需要 RAG / 向量数据库（P2 可引入）
- **原因**：
  - MVP 阶段不涉及大规模文档检索
  - 日报模板和规则可以硬编码或从数据库查询
  - 未来可引入：历史日报检索、运营知识库问答

### 需要结构化输出（Structured Output）
- LangGraph + Pydantic 确保 Agent 输出格式可控
- 日报生成器输出符合 Markdown/JSON schema 的结构化内容
- 价格监测 Agent 输出统一字段 schema

## 5. 为什么这样选

### 开发速度
- Python + FastAPI + LangGraph 组合在 AI Agent 项目中开发速度最快
- Ant Design 提供开箱即用的企业级 UI 组件
- LangGraph 减少 Agent 状态管理的手写代码量

### 成本
- 全部采用开源技术栈（零许可费用）
- PostgreSQL + pgvector 一站式数据库，减少运维成本
- LLM API 按量付费，MVP 阶段月调用量可控在 $200-$500

### 可维护性
- TypeScript 前端 + Python 后端的类型安全体系
- LangGraph 的状态图可视化，便于调试和修改 Agent 流程
- 模块化目录结构，每个 Agent 独立部署/升级

### 扩展性
- 主图 + 子图架构天然支持新增 Agent
- FastAPI 异步支持高并发
- Celery 任务队列可横向扩展 Worker 节点

### 招聘市场通用性
- React + Python 全栈组合在市场上人才储备充裕
- LangGraph 是新兴但增长最快的 Agent 框架
- PostgreSQL + Redis 是通用基础设施，工程师普遍熟悉

## 6. 项目结构

```
office-automation-agent/
├── README.md
├── docker-compose.yml
├── docker-compose.prod.yml
├── .env.example
├── .env
├── pyproject.toml
├── Makefile
│
├── backend/
│   ├── Dockerfile
│   ├── alembic.ini
│   ├── alembic/
│   │   ├── env.py
│   │   └── versions/
│   │
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py                     # FastAPI 入口
│   │   ├── config.py                   # 全局配置
│   │   ├── database.py                 # DB 连接
│   │   │
│   │   ├── agents/                     # LangGraph Agent 定义
│   │   │   ├── __init__.py
│   │   │   ├── master_graph.py         # 主图：意图检测 + 路由
│   │   │   ├── intent_detector.py      # 意图分类器
│   │   │   ├── state_schema.py         # 全局状态 Schema
│   │   │   │
│   │   │   ├── pricing_monitor/        # 竞品定价监测子图
│   │   │   │   ├── __init__.py
│   │   │   │   ├── graph.py
│   │   │   │   ├── nodes.py            # 爬虫节点、解析节点、存储节点
│   │   │   │   └── schemas.py
│   │   │   │
│   │   │   ├── daily_report/           # 日报生成子图
│   │   │   │   ├── __init__.py
│   │   │   │   ├── graph.py
│   │   │   │   ├── nodes.py            # 数据聚合节点、LLM 生成节点
│   │   │   │   └── schemas.py
│   │   │   │
│   │   │   ├── campaign_agent/         # 活动/广告自动化子图 (P1)
│   │   │   │   ├── __init__.py
│   │   │   │   ├── graph.py
│   │   │   │   ├── nodes.py
│   │   │   │   └── schemas.py
│   │   │   │
│   │   │   └── scheduler_agent/        # 任务调度子图
│   │   │       ├── __init__.py
│   │   │       ├── graph.py
│   │   │       ├── nodes.py
│   │   │       └── schemas.py
│   │   │
│   │   ├── api/                        # REST API
│   │   │   ├── __init__.py
│   │   │   ├── v1/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── router.py
│   │   │   │   ├── pricing.py          # 价格监测 API
│   │   │   │   ├── reports.py          # 日报 API
│   │   │   │   ├── campaigns.py        # 活动管理 API (P1)
│   │   │   │   ├── scheduler.py        # 调度器 API
│   │   │   │   └── dashboard.py        # Dashboard 数据 API
│   │   │   └── websocket.py            # WebSocket 实时推送
│   │   │
│   │   ├── services/                   # 业务逻辑层
│   │   │   ├── __init__.py
│   │   │   ├── pricing_service.py
│   │   │   ├── report_service.py
│   │   │   ├── campaign_service.py
│   │   │   ├── notification_service.py # 告警推送（邮件/飞书/钉钉/Slack）
│   │   │   └── scheduler_service.py
│   │   │
│   │   ├── models/                     # SQLAlchemy ORM 模型
│   │   │   ├── __init__.py
│   │   │   ├── competitor_price.py
│   │   │   ├── daily_report.py
│   │   │   ├── campaign.py
│   │   │   ├── task_schedule.py
│   │   │   └── alert_rule.py
│   │   │
│   │   ├── schemas/                    # Pydantic 请求/响应 Schema
│   │   │   ├── __init__.py
│   │   │   ├── pricing.py
│   │   │   ├── report.py
│   │   │   ├── campaign.py
│   │   │   └── common.py
│   │   │
│   │   ├── tasks/                      # Celery 任务
│   │   │   ├── __init__.py
│   │   │   ├── celery_app.py
│   │   │   ├── pricing_tasks.py
│   │   │   ├── report_tasks.py
│   │   │   └── campaign_tasks.py
│   │   │
│   │   └── utils/                      # 工具函数
│   │       ├── __init__.py
│   │       ├── llm_client.py           # LLM API 封装
│   │       ├── scraper.py              # 爬虫工具
│   │       ├── notification.py         # 通知工具
│   │       └── markdown_renderer.py    # 日报渲染
│   │
│   └── tests/
│       ├── __init__.py
│       ├── test_intent_detector.py
│       ├── test_pricing_agent.py
│       ├── test_report_agent.py
│       ├── test_scheduler_agent.py
│       └── test_api.py
│
└── frontend/
    ├── Dockerfile
    ├── package.json
    ├── tsconfig.json
    ├── vite.config.ts
    ├── index.html
    │
    └── src/
        ├── main.tsx
        ├── App.tsx
        ├── routes.tsx
        │
        ├── layouts/
        │   └── MainLayout.tsx
        │
        ├── pages/
        │   ├── Dashboard/
        │   │   └── index.tsx
        │   ├── PricingMonitor/
        │   │   ├── index.tsx
        │   │   └── ProductDetail.tsx
        │   ├── DailyReport/
        │   │   ├── index.tsx
        │   │   └── ReportEditor.tsx
        │   ├── Campaign/
        │   │   ├── index.tsx
        │   │   └── CampaignEditor.tsx
        │   ├── Scheduler/
        │   │   └── index.tsx
        │   └── Settings/
        │       └── index.tsx
        │
        ├── components/
        │   ├── AgentStatusBadge.tsx
        │   ├── PriceChart.tsx
        │   ├── AlertCard.tsx
        │   └── ReportPreview.tsx
        │
        ├── hooks/
        │   ├── usePricingData.ts
        │   ├── useReports.ts
        │   ├── useWebSocket.ts
        │   └── useTasks.ts
        │
        ├── services/
        │   └── api.ts
        │
        ├── stores/
        │   └── dashboardStore.ts
        │
        └── types/
            └── index.ts
```

## 7. 开发里程碑

### Week 1-2: 基础设施搭建
- [ ] 项目脚手架创建（FastAPI + React + Docker）
- [ ] PostgreSQL + Redis 本地环境搭建
- [ ] LangGraph 最小主图：意图检测 -> Echo 子图（验证架构）
- [ ] Alembic 数据库迁移脚本
- [ ] CI/CD 基础 pipeline（lint + test + build）

### Week 3-4: 竞品定价监测 Agent (P0)
- [ ] 爬虫 Agent 子图：URL 解析 -> Playwright 渲染 -> 数据提取
- [ ] 竞品价格 Schema 设计 + 数据库存储
- [ ] 价格变动检测逻辑（阈值触发）
- [ ] 通知服务接入（飞书/钉钉 Webhook）
- [ ] 定价监测 API 端点（CRUD）
- [ ] 前端价格监测页面（表格 + 趋势图）

### Week 5-6: 日报自动生成 Agent (P0)
- [ ] 数据聚合服务（销售数据、运营数据、竞品数据）
- [ ] LLM 日报生成节点（Prompt 模板工程）
- [ ] 日报渲染器（Markdown -> HTML -> PDF）
- [ ] 手动触发 + 自动定时触发日报生成
- [ ] 日报 API 端点
- [ ] 前端日报页面（预览 + 历史列表 + 导出）

### Week 7: 任务调度与运营任务 Agent (P0)
- [ ] APScheduler 定时任务管理器
- [ ] 任务 CRUD API
- [ ] 调度器 Agent 子图（接收 cron 表达式 -> 调度子 Agent）
- [ ] WebSocket 实时推送 Agent 运行状态
- [ ] 前端调度器页面 + Agent 状态看板

### Week 8: 集成测试、部署与文档
- [ ] 端到端集成测试
- [ ] Docker Compose 生产配置
- [ ] 部署文档 + API 文档（Swagger）
- [ ] 性能压测（爬虫并发、LLM 调用延迟）
- [ ] 上线准备会议

### P1 规划（Week 9-12）
- [ ] 活动/广告自动化 Agent
- [ ] 异常检测与告警 Agent
- [ ] 数据看板增强版
- [ ] 多平台数据桥接

## 8. 风险提示

| 风险类别 | 风险描述 | 概率 | 影响 | 缓解措施 |
|---------|---------|------|------|---------|
| 爬虫被封锁 | 竞品网站反爬机制升级，IP 被封 | 高 | 高 | 使用代理池 + 随机 User-Agent + 降低频率 + 备用 API |
| LLM 幻觉 | 日报生成中出现事实性错误（如数据对不上） | 中 | 高 | 结构化输出 + 数据校验节点 + 人工审核按钮 |
| LangGraph 稳定性 | 框架较新，可能存在 Bug 或 API 变更 | 中 | 中 | 固定版本 + 关注 changelog + 关键路径单元测试 |
| 定时任务延迟 | 多个 Agent 并发执行导致任务堆积 | 低 | 中 | Celery Worker 水平扩容 + 任务优先级队列 |
| 竞品网站改版 | 竞品网站 DOM 结构变化导致爬虫失效 | 高 | 中 | 爬虫异常告警 + 可视化选择器配置（非硬编码） |
| 数据安全 | 运营数据/定价策略泄露 | 低 | 高 | 敏感数据加密 + RBAC 权限控制 + 审计日志 |
| API 费用超支 | LLM API 调用量增长超出预期 | 中 | 中 | 设置配额 + 缓存 + 使用更便宜的模型做简单任务 |

## 9. CI/CD 设计

### 工具链
- **版本管理**：GitHub Flow（main + feature branches）
- **CI 平台**：GitHub Actions
- **代码质量**：Ruff（Python）/ ESLint + Prettier（TypeScript）
- **测试**：pytest（Python）/ Vitest（TypeScript）
- **安全扫描**：Bandit（Python）/ npm audit（Node）

### Pipeline 流程

```
PR Created
  +-- lint (Ruff / ESLint)
  +-- type-check (mypy / ts-check)
  +-- unit test (pytest / vitest)
  +-- security scan (Bandit / npm audit)
  +-- build check (Docker build test)

PR Merged to main
  +-- integration test (docker-compose up -> API test)
  +-- build & push Docker images to ECR
  +-- deploy to staging (auto)

Tag Release (v*)
  +-- full regression test
  +-- build & push Docker images
  +-- deploy to production (manual approval gate)
```

## 10. 部署方案

### 开发环境
```
docker-compose.yml
+-- postgres:15
+-- redis:7
+-- backend (hot reload)
|   +-- uvicorn --reload
|   +-- celery -A app.tasks worker
+-- frontend (Vite dev server)
+-- nginx (dev proxy)
```

### 生产环境 (AWS)

```
Internet -> CloudFront -> ALB
                         +-- ECS Fargate (Frontend - Nginx + React SPA)
                         +-- ECS Fargate (Backend API - FastAPI + Uvicorn)
                         +-- ECS Fargate (Celery Worker - 可水平扩展)
                         +-- ECS Fargate (Celery Beat - 定时调度器)
                         +-- RDS PostgreSQL (主库 + 只读副本)
                              +-- ElastiCache Redis
```

### 环境变量管理
- 开发环境：`.env` 文件（gitignored）
- 生产环境：AWS Secrets Manager + Parameter Store
- 敏感配置：第三方 API Key、数据库密码、JWT Secret

### 域名与 HTTPS
- 域名：`automation.example.com`（示例）
- SSL：Let's Encrypt + Nginx 反向代理自动续签

### 监控与日志
- **应用日志**：JSON format -> AWS CloudWatch Logs
- **指标**：Prometheus 暴露 `/metrics` -> Grafana 看板
- **告警**：PagerDuty / 飞书 Webhook（服务宕机、错误率 > 5%）
- **APM**：可选接入 Sentry / Datadog

## 11. 项目初始化命令

```bash
# 1. 创建项目目录
mkdir -p office-automation-agent && cd office-automation-agent

# 2. 初始化后端
python3.11 -m venv .venv
source .venv/bin/activate
pip install "fastapi[standard]" uvicorn langgraph langchain openai pydantic sqlalchemy alembic psycopg2-binary redis celery apscheduler playwright httpx beautifulsoup4 lxml python-dotenv pydantic-settings

# 3. 初始化前端
npm create vite@latest frontend -- --template react-ts
cd frontend
npm install antd @ant-design/icons axios zustand @tanstack/react-query recharts echarts echarts-for-react react-router-dom dayjs
cd ..

# 4. Docker 环境
cat > docker-compose.yml << 'EOF'
version: "3.9"
services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_DB: office_automation
      POSTGRES_USER: dev
      POSTGRES_PASSWORD: devpass
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

  redis:
    image: redis:7
    ports:
      - "6379:6379"

volumes:
  pgdata:
EOF

# 5. 数据库初始化
alembic init alembic
alembic revision --autogenerate -m "init"
alembic upgrade head

# 6. 启动开发服务
docker compose up -d postgres redis
# 终端1: uvicorn app.main:app --reload --port 8000
# 终端2: cd frontend && npm run dev
# 终端3: celery -A app.tasks.celery_app worker --loglevel=info
```
