# 办公流程自动化 Agent — Product PRD 文档

## 1. 产品概述

### 产品名称
**Azazie Office Automation Agent**（内部代号：AOA）

### 定位一句话
面向跨境电商企业的 AI Agent 办公流程自动化平台，用多 Agent 协作替代重复性人工运营操作。

### 目标用户
| 用户角色 | 描述 | 人数预估 |
|---------|------|---------|
| **运营经理** | 每日需要手动抓取竞品价格、制作日报、配置活动 | 3-5 人 |
| **市场投放专员** | 管理 Google Ads / Facebook Ads 投放，需要自动化调整 | 2-3 人 |
| **数据分析师** | 需要聚合多维度数据进行分析和报表产出 | 1-2 人 |
| **管理层** | 查看 Dashboard 和日报，做业务决策 | 2-3 人 |

### 核心痛点
1. **手工竞品监测耗时**：运营每天花 1-2 小时手动浏览竞品网站，记录价格变动
2. **日报撰写重复枯燥**：每天花 30-60 分钟从多个系统导出数据、拼接日报
3. **活动配置容易出错**：手动配置促销活动/广告组时容易漏设参数，导致活动失败
4. **信息孤岛**：运营数据分散在 Shopify、Google Ads、ERP 等多个系统，无统一视图
5. **响应滞后**：竞品降价 2-3 天后才被发现，丧失调价窗口

### 价值主张
"让 AI Agent 替你值守重复的运营工作，每天节省 2+ 小时，竞品变动即时感知，决策数据随时可得。"

## 2. 市场调研

### 市场现状
- 跨境电商 SaaS 市场规模在 2024 年达到 $128 亿，预计 2030 年达到 $398 亿（CAGR 20.4%）
- 电商运营自动化工具主要集中在：邮件营销(Klaviyo)、广告管理(AdEspresso)、客服(Zendesk)
- **竞品监测和运营流程自动化** 赛道尚处于早期，缺乏一站式解决方案
- Shopify 生态中有大量 App，但多数是单点工具，缺乏 Agent AI 驱动的工作流串联

### 用户需求趋势
1. **从"数据可视化"到"自动化执行"**：用户不再满足于看报表，希望系统直接执行操作
2. **AI Agent 接受度提升**：2024 年 ChatGPT/GPTs 教育了市场，用户对 AI 代理的信任度上升
3. **低代码/无配置偏好**：运营人员不愿写代码，希望自然语言即可驱动系统
4. **实时告警需求**：从 T+1 的日报转向实时变动通知

### 机会点分析
| 机会点 | 说明 | 优先级 |
|-------|------|-------|
| 跨境电商竞品监测真空 | 绝大多数竞品监测工具面向国内市场(Alexa/SimilarWeb)，跨境垂直领域空白 | P0 |
| LLM 驱动的工作流编排 | 传统 RPA 需要录制/编写脚本，LLM Agent 可自然语言驱动 | P0 |
| 多 Agent 协作的价值差 | 单 Agent 能力有限，多 Agent 协作可覆盖完整业务流程 | P0 |
| 中国企业出海工具热 | 国内 SaaS 出海和服务出海企业数量激增，对运营效率工具需求旺盛 | P1 |

## 3. 竞品分析

### 竞品 1：Prisync
| 维度 | 内容 |
|------|------|
| **定位** | 跨境电商竞品定价与价格追踪 SaaS |
| **优点** | 竞品监测功能成熟；支持多店铺；价格历史图表完善 |
| **缺点** | 价格高($49/月起)；不涉足运营自动化；不支持日报生成；无 AI 能力 |
| **可借鉴** | 价格监测的数据展示方式、告警规则设计 |
| **差异化机会** | 集成 AI Agent 工作流，从"监测"升级到"监测+分析+执行" |

### 竞品 2：Klaviyo
| 维度 | 内容 |
|------|------|
| **定位** | 电商营销自动化平台（邮件 + SMS） |
| **优点** | 自动化流程设计器非常直观；强大的用户分群；与 Shopify 深度集成 |
| **缺点** | 专注营销自动化，不覆盖竞品监测和日报；价格较高 |
| **可借鉴** | 可视化流程设计器（Flow Builder）的交互模式 |
| **差异化机会** | 覆盖营销自动化之外的运营环节，做全链路自动化 |

### 竞品 3：Zapier / Make (Integromat)
| 维度 | 内容 |
|------|------|
| **定位** | 通用自动化平台（App 互联 + 工作流） |
| **优点** | 支持上千个 App 集成；无代码配置；稳定可靠 |
| **缺点** | 能力局限在数据搬运；无 AI 分析能力；复杂逻辑需大量步骤编排 |
| **可借鉴** | Webhook/API 集成模式；任务编排的 DAG 思维 |
| **差异化机会** | AI Agent 主动决策（不只搬运数据，还分析数据并执行操作） |

### 竞品 4：Shopify Flow
| 维度 | 内容 |
|------|------|
| **定位** | Shopify 官方自动化工具 |
| **优点** | 免费；与 Shopify 原生集成；触发器+条件+动作的模板化设计 |
| **缺点** | 仅限 Shopify 生态；不支持外部竞品监测；无 AI 能力 |
| **可借鉴** | 触发器(Templates)的设计方式，降低用户上手门槛 |
| **差异化机会** | 跨平台能力（Shopify + 竞品网站 + Google Ads + 飞书/钉钉） |

### 差异化总结

| 维度 | 竞品 | 我们的差异化 |
|------|------|-------------|
| 竞品监测 | Prisync | + AI 分析 + 自动调价建议 |
| 营销自动化 | Klaviyo | + 运营流程 + 日报生成 |
| 通用自动化 | Zapier | + AI Agent 决策 + 自然语言驱动 |
| 平台绑定 | Shopify Flow | + 跨平台 + 多 Agent 编排 |

## 4. MVP 定义

### P0：MVP 核心功能（必须上线）
| 模块 | 优先级 | 工作量估算 |
|------|--------|-----------|
| 多 Agent 编排引擎（主图+子图） | P0 | 2 周 |
| 竞品定价监测 Agent | P0 | 2 周 |
| 日报自动生成 Agent | P0 | 2 周 |
| 任务调度 Agent | P0 | 1 周 |
| 基础 Dashboard | P0 | 1 周 |
| 飞书/钉钉通知接入 | P0 | 0.5 周 |

### P1：延后功能
| 模块 | 优先级 | 说明 |
|------|--------|------|
| 活动/广告自动化配置 Agent | P1 | 需要对接 Shopify/Google Ads API |
| 异常检测与告警 Agent | P1 | 基于统计模型的历史异常识别 |
| Dashboard 增强版 | P1 | 交互式图表、自定义看板 |
| 多平台数据桥接 | P1 | ERP/OMS/CRM 对接 |

### P2：远期规划
| 模块 | 优先级 | 说明 |
|------|--------|------|
| AI 决策建议 Agent | P2 | 定价/广告出价策略建议 |
| 多语言翻译 Agent | P2 | 商品描述自动翻译 |
| 供应链协同 Agent | P2 | 库存监测与补货 |
| 用户行为分析 Agent | P2 | 转化漏斗、用户分群 |

### 明确不做什么
- 不开发电商平台功能
- 不开发 CRM/ERP 系统
- 不开发移动端 App
- 不开发实时客服系统
- 不自己做 LLM（调用第三方 API）

## 5. 功能详细设计

### 5.1 多 Agent 编排引擎

| 项目 | 内容 |
|------|------|
| **功能描述** | LangGraph 主图接收用户输入 -> 意图检测 -> 路由到子 Agent -> 聚合结果返回 |
| **用户价值** | 用户只需用自然语言描述需求，系统自动分配到正确的 Agent 执行 |
| **输入** | 用户自然语言指令，如："检查 XX 婚纱今天有没有降价"、"生成昨天的日报" |
| **输出** | Agent 执行结果（结构化数据 + 自然语言回复） |
| **关键逻辑** | 1. 意图分类（LLM + Few-shot） -> 2. 参数提取 -> 3. 子图路由 -> 4. 执行 -> 5. 结果格式化 |

### 5.2 竞品定价监测 Agent

| 项目 | 内容 |
|------|------|
| **功能描述** | 定时爬取竞品网站上指定 SKU 的价格，对比上次价格，如有变动触发告警 |
| **用户价值** | 不再需要人工浏览竞品网站，价格变动即时感知 |
| **输入** | 竞品 URL 列表（带 CSS 选择器配置）、监测频率、价格阈值 |
| **输出** | 价格变动记录、趋势图表、告警通知 |
| **关键逻辑** | 1. Playwright 渲染页面 -> 2. BeautifulSoup 提取价格 -> 3. 清洗标准化 -> 4. 与上次价格对比 -> 5. 超阈值触发告警 -> 6. 写入数据库 |

### 5.3 日报自动生成 Agent

| 项目 | 内容 |
|------|------|
| **功能描述** | 每日定时（或手动触发）聚合销售数据、运营数据、竞品数据，由 LLM 生成结构化的日报 |
| **用户价值** | 从手动拼接日报解放，日报质量和一致性提升，且支持定时自动发送 |
| **输入** | 日报模板配置、数据源（DB/API）、时间范围 |
| **输出** | Markdown/HTML/PDF 格式日报 |
| **关键逻辑** | 1. 从数据库查询当日数据 -> 2. 聚合计算 KPI -> 3. LLM Prompt 填充模板 -> 4. 渲染器生成最终格式 -> 5. 自动推送到飞书/钉钉/邮件 |

### 5.4 任务调度 Agent

| 项目 | 内容 |
|------|------|
| **功能描述** | 基于 cron 表达式的定时任务管理，支持对任意 Agent 进行调度 |
| **用户价值** | 灵活配置各种定时任务（如：每小时检查竞品价格、每天早上 9 点生成日报） |
| **输入** | cron 表达式 + 目标 Agent + 参数 |
| **输出** | 任务执行日志、执行状态、WebSocket 实时推送 |
| **关键逻辑** | 1. APScheduler 接收 cron 配置 -> 2. 触发目标 Agent 子图 -> 3. 记录执行状态 -> 4. 推送结果 |

### 5.5 活动/广告自动化配置 Agent (P1)

| 项目 | 内容 |
|------|------|
| **功能描述** | 通过自然语言指令或模板创建/修改 Shopify 促销活动或 Google Ads 广告组 |
| **用户价值** | 活动配置从 30 分钟缩短到 30 秒，减少人为配置错误 |
| **输入** | 自然语言："创建一个 7 天夏季促销，所有婚纱 8 折" |
| **输出** | 活动创建结果、API 返回详情 |
| **关键逻辑** | 1. 意图解析 -> 2. 参数提取（折扣率、时间、范围） -> 3. 调用 Shopify/Google Ads API -> 4. 验证结果 |

## 6. 用户流程

### 核心流程 1：竞品定价监测

```
用户登录 Dashboard
  |
  +-> 进入"定价监测"页面
  |     |
  |     +-> 添加竞品产品（输入 URL + CSS 选择器）
  |     +-> 系统自动抓取一次验证配置是否正确
  |     +-> 设置监测频率（如每 2 小时）
  |     +-> 设置价格变动告警阈值（如降幅 > 5%）
  |
  +-> 系统按调度执行：
  |     +-> Playwright 渲染竞品页面
  |     +-> 提取价格并存储
  |     +-> 对比历史价格
  |     +-> 如有变动 -> 发送飞书/钉钉告警
  |
  +-> 用户收到告警 -> 登录查看价格趋势 -> 决定是否调价
```

### 核心流程 2：日报自动生成

```
用户进入"日报"页面
  |
  +-> 配置日报模板：
  |     +-> 选择数据源（销售额、订单量、竞品价格等）
  |     +-> 选择日报格式（Markdown / PDF）
  |     +-> 设置自动发送时间（如每天 09:00）
  |     +-> 设置接收人（飞书群/邮件列表）
  |
  +-> 每日定时触发：
  |     +-> Agent 聚合数据
  |     +-> LLM 生成日报正文
  |     +-> 渲染最终格式
  |     +-> 推送到配置的渠道
  |
  +-> 用户可手动触发即时生成
  +-> 用户查看历史日报列表，可重新发送
```

### 核心流程 3：活动自动化配置 (P1)

```
用户在聊天界面输入："创建一个 7 天夏季促销"
  |
  +-> 意图检测 Agent 识别为 "创建促销活动"
  +-> 参数提取 Agent 解析：
  |     +-> 活动类型 = 折扣促销
  |     +-> 折扣力度 = 需确认
  |     +-> 时间范围 = 7 天
  |     +-> 商品范围 = 需确认
  |
  +-> Agent 反问确认："请确认：为所有婚纱设置 8 折，持续 7 天？"
  +-> 用户确认
  +-> Agent 调用 Shopify API 创建活动
  +-> 返回创建结果 + 活动链接
```

## 7. 页面结构设计

### 页面清单

| # | 页面 | 路由 | P0/P1 | 说明 |
|---|------|------|-------|------|
| 1 | 登录页 | `/login` | P0 | 账号密码 / SSO 登录 |
| 2 | Dashboard 首页 | `/dashboard` | P0 | 系统概览：Agent 运行状态、今日告警数、日报状态 |
| 3 | 定价监测 | `/pricing` | P0 | 竞品列表、价格趋势图、告警历史 |
| 4 | 定价监测-新增 | `/pricing/new` | P0 | 添加竞品 URL 和配置 |
| 5 | 定价监测-详情 | `/pricing/:id` | P0 | 单个竞品的详细趋势和价格历史 |
| 6 | 日报管理 | `/reports` | P0 | 日报列表、手动生成、定时配置 |
| 7 | 日报编辑 | `/reports/template` | P0 | 日报模板配置 |
| 8 | 日报预览 | `/reports/:id` | P0 | 预览已生成的日报 |
| 9 | 调度任务 | `/scheduler` | P0 | 定时任务列表、状态、执行日志 |
| 10 | 调度任务-新建 | `/scheduler/new` | P0 | 创建定时任务（cron + Agent） |
| 11 | 活动管理 | `/campaigns` | P1 | 活动列表、状态、自动化配置 |
| 12 | 设置页 | `/settings` | P0 | 通知渠道配置、API Key、用户管理 |

### 页面跳转关系

```
/login
  |
  +-> /dashboard  (主导航页)
        |
        +-> /pricing
        |     +-> /pricing/new
        |     +-> /pricing/:id
        |
        +-> /reports
        |     +-> /reports/template
        |     +-> /reports/:id
        |
        +-> /scheduler
        |     +-> /scheduler/new
        |
        +-> /campaigns (P1)
        |
        +-> /settings
```

### HTML 原型描述 (文字版)

#### Dashboard 首页
```
+--------------------------------------------------------------+
|  Azazie Automation  [Dashboard] [Pricing] [Reports] [Tasks]  |
+--------------------------------------------------------------+
|                                                               |
|  +--------+ +--------+ +--------+ +--------+                  |
|  | Agents  | | Today  | | Active | | Reports|                  |
|  | Online  | | Alerts | | Tasks  | | Today  |                  |
|  |   4/4   | |   3    | |   5    | |   1    |                  |
|  +--------+ +--------+ +--------+ +--------+                  |
|                                                               |
|  Recent Activity                            [View All >]     |
|  +--------------------------------------------------------+  |
|  | 09:15 | [Pricing] XX Dress - Price dropped 12%        |  |
|  | 09:00 | [Report] Daily Report for 2026-05-07 generated |  |
|  | 08:30 | [Alert] Competitor A price below threshold     |  |
|  | 07:00 | [Task] Price check cron job completed. 5/5 OK |  |
|  +--------------------------------------------------------+  |
|                                                               |
|  Price Trends (Last 7 Days)                                   |
|  [=========================================]  (chart)         |
+--------------------------------------------------------------+
```

#### 定价监测页面
```
+--------------------------------------------------------------+
|  Pricing Monitor  [+ Add Product]                             |
+--------------------------------------------------------------+
|                                                               |
|  Filters: [All Products] [With Changes Only]  [Search...]    |
|                                                               |
|  +--------------------------------------------------------+  |
|  | Product          | Our $ | Competitor A | Competitor B |  |
|  |------------------|-------|--------------|--------------|  |
|  | Lace A-Line      | $299  | $259 (-10%)! | $289 (-3%)  |  |
|  | Ball Gown        | $399  | $379 (-5%)!  | $399        |  |
|  | Mermaid Silhouette| $349 | $329         | $359 (+3%)  |  |
|  +--------------------------------------------------------+  |
|                                                               |
|  Alerts (3 new)                                               |
|  +--------------------------------------------------------+  |
|  | ! Lace A-Line dropped 10% below our price (threshold:5%)|  |
|  | ! Ball Gown dropped 5% below our price                   |  |
|  +--------------------------------------------------------+  |
+--------------------------------------------------------------+
```

## 8. 数据结构设计

### 核心表结构

#### competitor_products（竞品产品表）
```sql
CREATE TABLE competitor_products (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name            VARCHAR(255) NOT NULL,
    url             TEXT NOT NULL,
    css_selector    TEXT,          -- 价格 CSS 选择器
    image_url       TEXT,
    competitor_name VARCHAR(100),  -- 竞品店铺名
    category        VARCHAR(100),  -- 产品分类
    is_active       BOOLEAN DEFAULT TRUE,
    created_at      TIMESTAMPTZ DEFAULT NOW(),
    updated_at      TIMESTAMPTZ DEFAULT NOW(),
    UNIQUE(url)
);
```

#### price_history（价格历史表）
```sql
CREATE TABLE price_history (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id      UUID REFERENCES competitor_products(id) ON DELETE CASCADE,
    price           DECIMAL(10, 2) NOT NULL,
    currency        VARCHAR(3) DEFAULT 'USD',
    discount_percent DECIMAL(5, 2),  -- 折扣百分比
    source          VARCHAR(50),      -- 数据来源：scraped / api
    raw_data        JSONB,           -- 原始 HTML/JSON 数据
    scraped_at      TIMESTAMPTZ DEFAULT NOW(),
    INDEX idx_product_scraped (product_id, scraped_at DESC)
);
```

#### price_alerts（价格告警表）
```sql
CREATE TABLE price_alerts (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    product_id      UUID REFERENCES competitor_products(id) ON DELETE CASCADE,
    old_price       DECIMAL(10, 2),
    new_price       DECIMAL(10, 2),
    change_percent  DECIMAL(5, 2),
    change_type     VARCHAR(20) CHECK (change_type IN ('drop', 'rise', 'cross_threshold')),
    threshold       DECIMAL(5, 2),
    is_read         BOOLEAN DEFAULT FALSE,
    notified_at     TIMESTAMPTZ,
    created_at      TIMESTAMPTZ DEFAULT NOW()
);
```

#### daily_reports（日报表）
```sql
CREATE TABLE daily_reports (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    title           VARCHAR(255),
    report_date     DATE NOT NULL,
    summary         TEXT,                    -- LLM 生成的摘要
    content_md      TEXT,                    -- Markdown 正文
    content_html    TEXT,                    -- HTML 渲染版（备选）
    metrics         JSONB,                   -- { revenue: 12345, orders: 89, ... }
    status          VARCHAR(20) DEFAULT 'draft' CHECK (status IN ('draft', 'published', 'sent')),
    generated_by    VARCHAR(50),             -- 'scheduled' | 'manual'
    created_at      TIMESTAMPTZ DEFAULT NOW(),
    sent_at         TIMESTAMPTZ,
    UNIQUE(report_date)
);
```

#### task_schedules（定时任务表）
```sql
CREATE TABLE task_schedules (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name            VARCHAR(255) NOT NULL,
    agent_type      VARCHAR(50) NOT NULL,   -- 'pricing_monitor' | 'daily_report' | 'campaign'
    cron_expression VARCHAR(100) NOT NULL,
    params          JSONB DEFAULT '{}',      -- 任务参数
    is_active       BOOLEAN DEFAULT TRUE,
    last_run_at     TIMESTAMPTZ,
    last_status     VARCHAR(20) DEFAULT 'pending' CHECK (last_status IN ('pending', 'running', 'success', 'failed')),
    created_at      TIMESTAMPTZ DEFAULT NOW(),
    updated_at      TIMESTAMPTZ DEFAULT NOW()
);
```

#### alert_channels（告警渠道表）
```sql
CREATE TABLE alert_channels (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    channel_type    VARCHAR(20) NOT NULL CHECK (channel_type IN ('feishu', 'dingtalk', 'slack', 'email', 'webhook')),
    name            VARCHAR(255),
    config          JSONB NOT NULL,          -- { webhook_url, secret, token }
    is_active       BOOLEAN DEFAULT TRUE,
    created_at      TIMESTAMPTZ DEFAULT NOW()
);
```

### 核心索引
```sql
-- 价格历史查询优化
CREATE INDEX idx_price_history_product_time ON price_history(product_id, scraped_at DESC);

-- 告警查询优化
CREATE INDEX idx_price_alerts_unread ON price_alerts(is_read, created_at DESC);

-- 日报查询优化
CREATE INDEX idx_daily_reports_date ON daily_reports(report_date DESC);

-- 调度任务查询
CREATE INDEX idx_task_schedules_active ON task_schedules(is_active, next_run_at);
```

### 数据流示意

```
[Scraper Agent] --(insert)--> price_history
                                  |
[Compare Logic] --(if changed)--> price_alerts
                                     |
[Notification Service] --(send)--> alert_channels
                                     |
[Daily Report Agent] --(aggregate)--> daily_reports
                                            |
[Render Service] ------------> Markdown / HTML / PDF
```

## 9. 技术依赖说明

### 核心依赖

| 依赖 | 用途 | 版本要求 | 许可 |
|------|------|---------|------|
| **Python 3.11+** | 后端语言 | >= 3.11 | PSF |
| **FastAPI** | REST API 框架 | >= 0.110 | MIT |
| **LangGraph** | Agent 编排框架 | >= 0.1.0 | MIT |
| **LangChain** | LLM 调用抽象 | >= 0.2.0 | MIT |
| **OpenAI SDK** | GPT-4 API 调用 | >= 1.0 | MIT |
| **Playwright** | 浏览器自动化爬虫 | >= 1.40 | Apache 2.0 |
| **SQLAlchemy 2.0** | ORM | >= 2.0 | MIT |
| **Alembic** | 数据库迁移 | >= 1.13 | MIT |
| **Celery** | 异步任务队列 | >= 5.3 | BSD |
| **Redis** | 缓存 + 消息队列 | >= 7.0 | BSD |
| **PostgreSQL** | 主数据库 | >= 15 | PostgreSQL |
| **React 18** | 前端框架 | >= 18 | MIT |
| **Ant Design** | UI 组件库 | >= 5.0 | MIT |
| **Zustand** | 状态管理 | >= 4.0 | MIT |
| **TanStack Query** | 数据请求 | >= 5.0 | MIT |
| **Recharts** | 图表库 | >= 2.0 | MIT |
| **ECharts** | 高级图表 | >= 5.0 | Apache 2.0 |
| **Docker** | 容器化 | >= 24.0 | Apache 2.0 |
| **Nginx** | 反向代理 | >= 1.24 | BSD |

### 外部服务依赖

| 服务 | 用途 | 付费模式 | 月费预估 |
|------|------|---------|---------|
| **OpenAI API** (GPT-4) | 意图检测、日报生成 | 按 Token 计费 | $200-$500 |
| **AWS ECS / RDS** | 生产部署 | 按资源计费 | $200-$800 |
| **飞书/钉钉 Webhook** | 通知推送 | 免费 | $0 |
| **代理 IP 池 (可选)** | 反爬绕过 | 按量付费 | $50-$200 |

### 环境要求

| 环境 | 配置要求 |
|------|---------|
| **开发笔记本** | 8GB+ RAM, Python 3.11, Node 18+, Docker |
| **CI Runner** | 2 vCPU, 4GB RAM, Docker |
| **生产（最小）** | 2 vCPU, 4GB RAM (API), 2 vCPU, 4GB RAM (Worker) |
| **生产（推荐）** | 4 vCPU, 8GB RAM (API x2), 4 vCPU, 8GB RAM (Worker x2) |

## 10. 风险分析

| 风险 | 概率 | 影响 | 等级 | 应对策略 |
|------|------|------|------|---------|
| **LLM 幻觉导致日报数据错误** | 中 | 高 | 高 | 所有数字字段在 LLM 输出后做二次校验；LLM 只写文案，数据填充在后端完成 |
| **竞品网站反爬封锁** | 高 | 高 | 高 | 代理池 + 多 User-Agent + 模拟人类行为（随机延迟、鼠标轨迹）+ 备用 API |
| **LangGraph 框架不成熟** | 中 | 中 | 中 | 固定版本 + 写单元测试覆盖关键路径 + 预研 Plan B（直接 LangChain Agent） |
| **API 费用超支** | 中 | 中 | 中 | LLM 调用配额 + 日志监控 + 缓存频繁查询 + 简单任务用 GPT-4o-mini |
| **数据安全/隐私泄露** | 低 | 高 | 中 | 所有 API Key 通过 AWS Secrets Manager；数据库加密；审计日志；RBAC |
| **运营人员拒绝使用** | 中 | 高 | 高 | 早期深度参与设计；MVP 快速迭代获取反馈；降低使用门槛（自然语言交互） |
| **Shopify/Google Ads API 变更** | 低 | 中 | 低 | 隔离 API 调用层，方便适配升级 |
| **爬虫数据质量不稳定** | 中 | 中 | 中 | 数据清洗+异常值过滤；手动核验入口；置信度评分 |

### LLM 幻觉专项防护
- **结构化输出优先**：使用 Pydantic 定义输出 Schema，强迫 LLM 输出符合结构
- **数据与文案分离**：数字指标直接从数据库查询填充，LLM 只负责文字组织和摘要
- **置信度标记**：对 LLM 生成的结论附置信度（如"数据来源：AI 分析，仅供参考"）
- **人工审核兜底**：日报生成后自动发送前，支持人工预览和修改

## 11. 商业化设计

### 收费模式（面向 B2B SaaS）

| 套餐 | 价格（月） | 配额 | 目标用户 |
|------|-----------|------|---------|
| **Starter** | $99 | 2 个竞品监测 SKU + 日报生成 + 5 个调度任务 | 小型卖家 |
| **Professional** | $299 | 20 个竞品 SKU + 日报 + 告警 + 50 个任务 + 活动自动化 | 成长型卖家 |
| **Enterprise** | $799+ | 无限 SKU + 全部功能 + 定制 Agent + SLA + 专属部署 | 大型品牌商 |

### 付费点与转化路径
1. **免费试用**：14 天全功能试用（限量 5 个 SKU）
2. **功能付费墙**：
   - 竞品监测数量是核心付费计数维度
   - 活动自动化仅在 Professional 及以上提供
   - 自定义 Agent（P2）作为 Enterprise 增值功能
3. **增值服务**：
   - 专用代理 IP 池（$50/月）
   - 定制日报模板设计（一次性 $500）
   - 私有化部署（Enterprise 专属）

### 客户获取渠道
- Shopify App Store 上架
- 跨境电商卖家社区（雨果网、卖家圈）
- 行业展会/线上研讨会
- 与 ERP 服务商合作分销

## 12. 指标体系（KPI）

### 产品指标

| 指标 | 定义 | 目标值（上线 3 个月） | 监测方式 |
|------|------|---------------------|---------|
| **DAU** | 日活跃用户数 | > 20（团队内） | 埋点 |
| **任务执行成功率** | Agent 任务成功/总任务 | > 95% | 系统日志 |
| **日报采用率** | 自动发送日报数 / 可发送日 | > 90% | 系统统计 |
| **告警准确率** | 有效告警 / 总告警数 | > 85% | 用户反馈标记 |
| **爬虫成功率** | 成功抓取/总抓取次数 | > 90% | 系统日志 |
| **用户留存率** | 次日 / 7日 / 30日留存 | > 80% / > 60% / > 40% | 埋点 |

### 业务指标

| 指标 | 定义 | 目标值 | 监测方式 |
|------|------|-------|---------|
| **用户时间节省** | 使用前后每日节省分钟数 | > 90 分钟/天 | 用户调研 |
| **竞品响应时间** | 从竞品调价到系统告警的延迟 | < 30 分钟 | 系统日志 |
| **活动配置错误率** | 自动配置 vs 手动配置错误率对比 | 降低 80% | 对比测试 |
| **NPS** | 用户净推荐值 | > 50 | 定期调研 |

### 技术指标

| 指标 | 目标值 |
|------|-------|
| API 响应时间（P95） | < 500ms（非 LLM 调用） |
| Agent 任务完成时间（P95） | < 5 分钟 |
| 系统可用性（SLA） | > 99.5% |
| 爬虫单次执行时间 | < 30 秒 |
| LLM 日报生成时间 | < 60 秒 |

## 13. 与研发协作说明

### 协作流程
```
Product -> PRD 文档 -> 研发评审会 -> 技术设计评审 -> 开发 -> Code Review -> 测试 -> 上线
```

### 关键协作节点

| 节点 | 产出 | 参与方 | 频率 |
|------|------|--------|------|
| **Sprint 规划** | JIRA Ticket + 估算 | PM + 研发 | 每 2 周 |
| **技术设计评审** | 技术设计文档 | 架构师 + 全栈 | 新模块启动前 |
| **DEMO 演示** | 可运行 Demo | 全员 | 每 Sprint 末 |
| **Bug Bash** | Bug 清单 | 全员 | 上线前 1 周 |
| **上线评审** | 上线 Checklist | PM + 研发 + QA | 上线前 |

### 研发注意事项

1. **LangGraph 版本锁定**：框架 API 仍在演进，在 `pyproject.toml` 中锁定精确版本
2. **爬虫模块可插拔**：爬虫选择器不要硬编码，支持通过 API 动态更新
3. **LLM 调用加缓存**：相同 Prompt + 相同数据避免重复调用，设置 TTL 缓存
4. **所有 Agent 输出可溯**：每一步操作都写日志到 `agent_execution_log` 表，用于 Debug
5. **前端考虑暗黑模式**：运营人员可能长时间使用，且可能在晚上查看告警
6. **WebSocket 断线重连**：前端需要实现自动重连 + 指数退避
7. **敏感信息脱敏**：日志中不要打印 API Key 和数据库密码

### 交付物清单

| 交付物 | 负责人 | 验收标准 |
|--------|-------|---------|
| Planner 文档 | PM | 技术评审通过 |
| PRD 文档 | PM | 干系人确认 |
| 架构设计文档 | 架构师 | 技术评审通过 |
| API 文档 (Swagger) | 后端 | 自动生成 + 手动补充说明 |
| Docker Compose 配置 | 后端 | 开发环境一键启动 |
| 测试报告 | QA | 覆盖率 > 80%, 所有 P0 用例通过 |
| 部署手册 | DevOps | 运维可独立完成部署 |
| 用户手册 | PM | 运营人员可自助上手 |
