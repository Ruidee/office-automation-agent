# ⚙️ 办公流程自动化 Agent — 多 Agent 编排系统

> **作品集项目** | 完整展示 AI 产品经理的"多 Agent 协作设计"能力

---

## 项目简介

基于 **LangGraph 多 Agent 架构** 的办公自动化系统，用 1 个编排主图 + 多个独立子图替代重复性人工运营操作。

覆盖场景：竞品定价监测、活动与广告配置、日报自动生成、运营任务调度。

## 技术栈

| 技术 | 用途 |
|------|------|
| **LangGraph** | 多 Agent 编排引擎（主图+子图） |
| **FastAPI** | 后端 API |
| **React + TypeScript** | 前端 Dashboard |
| **PostgreSQL + pgvector** | 业务数据 + 向量检索 |
| **Redis** | 任务队列 + 缓存 |
| **Docker Compose** | 本地部署 |

## 文档导航

| 文件 | 内容 | 展示的 PM 能力 |
|------|------|---------------|
| [planner.md](./planner.md) | 技术规划：Agent 架构设计、子图拆解、协作规范 | 多 Agent 系统设计 |
| [prd.md](./prd.md) | 产品需求：痛点分析、功能设计、评估指标、商业化 | 产品定义 + ROI |

## 核心 AI PM 决策要点

```
为什么用多 Agent 而不是一个 LLM 搞定？
  → 不同任务需要不同能力（监测 vs 生成 vs 调度），
    拆成独立子图可以单独优化、单独测试。

Agent 之间怎么通信？
  → 统一 State Schema（所有子图输入输出格式一致）
  → 每个子图实现 can_handle() + execute()
  → 错误处理统一规范（错误码 + 降级方案）

怎么评估多 Agent 系统的效果？
  → 第一层：单个 Agent 能力（Precision/Recall/Latency）
  → 第二层：Agent 协作效率（路由准确率/端到端延迟）
  → 第三层：业务效果（转人工率/任务完成率）
```

---

*这是 AI 产品经理作品集项目之一。更多项目：*
- [私人医生助手](https://github.com/Ruidee/private-doctor-assistant)
- [企业 RAG 知识库客服](https://github.com/Ruidee/enterprise-kb-cs)
