# Loom

Loom 是一个面向深度学习实验室的实验运营原型系统，聚焦三件事：

- 实验室资产统一托管
- 全流程任务提交与运行追踪
- 结果可追溯与可复现

主要解决的问题是：

中小型实验室常常以手动设计实验，配置环境，运行实验，导致

# 当前状态

当前仓库处于 **v0.1 原型设计/收敛阶段**，以架构和边界定义为主。

---

## 架构口径（v0.1）

### 1) 内核层与 FastAPI 的关系

- **内核层（Kernel Core）**：framework-agnostic 的核心能力层，向 `CLI/SDK/Web 后端` 提供统一接口并屏蔽下层实现。
- **FastAPI（v0.1）**：当前用于控制器/交互侧的原型实现手段，不等价于“内核由 FastAPI 定义”。

### 2) 分层结构（当前方案）

- `shared`
- `domain`（五模块：`assets`、`execution`、`orchestration`、`traceability`、`interaction_context`）
- `policy`
- `application`
- `ports`
- `adapters`

---

## v0.1 关注范围

- 单体控制面优先（先保证结构清晰与边界稳定）
- 资源托管、任务运行、实验编排、追溯闭环四条主线
- 文档驱动的目录与模块边界落地

---

## 当前不做（v0.1）

- 不做微服务拆分落地（仅预留可拆分边界）
- 不做完整 Web UI/SDK 产品化交付
- 不做复杂分布式训练编排与高阶调度策略

---

## 文档入口

请优先阅读以下文档：

- `DOCUMENTS/v0.1/GLOBAL/总体架构.md`
- `DOCUMENTS/v0.1/GLOBAL/内核层总体架构与目录组织方案.md`
- `DOCUMENTS/v0.1/GLOBAL/技术选型.md`



---

## 协作约定

- 先更新/对齐文档，再推进实现。
- 涉及架构边界变更时，必须同步更新 `DOCUMENTS/v0.1/GLOBAL` 对应文档。
- 避免在 README 写入未落地的大范围承诺。

---

## License

Apache 2.0
