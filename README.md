# Loom

Loom 是一个面向深度学习实验室的实验运营原型系统，聚焦三件事：

- 资产统一登记与关联
- 任务提交与运行追踪
- 结果可追溯与可复现

当前仓库处于 **v0.1 原型设计/收敛阶段**，以架构和边界定义为主。

---

## 当前状态（请先看）

- 这是一个 **文档优先** 的开源项目，核心设计在 `DOCUMENTS/v0.1/GLOBAL`。
- v0.1 的目标是做出最小可用闭环（MVP），不是一次性做成完整平台。
- README 仅描述当前已确认范围，不包含远期功能承诺。

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

## 文档入口（权威来源）

请优先阅读以下文档：

- `DOCUMENTS/v0.1/GLOBAL/总体架构.md`
- `DOCUMENTS/v0.1/GLOBAL/内核层总体架构与目录组织方案.md`
- `DOCUMENTS/v0.1/GLOBAL/技术选型.md`

---

## 目录（当前）

```text
loom/
  DOCUMENTS/
    v0.1/
      GLOBAL/
  apps/
    controller/
    cli/
  core/
    db/
    models/
    scheduler/
    protocols/
```

说明：`core/` 现有目录是历史结构；目标结构以 `GLOBAL` 文档中定义的分层方案为准。

---

## 协作约定

- 先更新/对齐文档，再推进实现。
- 涉及架构边界变更时，必须同步更新 `DOCUMENTS/v0.1/GLOBAL` 对应文档。
- 避免在 README 写入未落地的大范围承诺。

---

## License

Apache 2.0
