# ForgeAI · 工程文档模板

> Vibe Coding 时代的 AI 友好型工程文档框架，用于从 0 到 1 启动新项目的需求、设计、规范和执行基线。

## 1. 这是什么

ForgeAI 是一套面向 AI 协作开发（Vibe Coding）的工程文档骨架。它由三类资产组成：

- **一套编号化的设计文档模板**（`docs/00-17` + `docs/18-云服务器生产部署手册(模板).md`），覆盖产品概述、需求、架构、领域、数据、API、UI、组件、规范、部署、测试与 RoadMap。
- **一份面向 AI 的协作协议**（`docs/AGENT-GUIDE.md`），约定会话启动、文档路由、任务状态、恢复点和收尾校验。
- **一份新项目初始化引导**（`docs/INIT-GUIDE.md`），当衍生项目第一次使用模板时，驱动 AI 和用户把所有占位符一次性补齐。

模板本身**技术栈中立**，适用于 Web、移动端、小程序等多形态项目；技术选型在新项目启动时由 `INIT-GUIDE.md` 向用户询问并落位到 `docs/03-系统架构设计(SAD).md` §2。

## 2. 何时该用 ForgeAI

- 需要在 Vibe Coding 流程中为 AI 提供清晰需求、设计、约束的新项目。
- 希望把「设计文档 / 任务台账 / 工程规范」作为单一事实来源来约束 AI 产出的项目。
- 希望跨项目复用同一套编号、同一套 FR/NFR/DR/ADR 约定、同一套会话协议的个人或小团队。

## 3. 何时不该用

- 一次性脚本、PoC 或学习代码：文档开销远大于收益。
- 已有自己成熟的文档体系的团队：直接套用 ForgeAI 的编号会与存量冲突。
- 需要严格遵循组织模板（如客户要求的特定 SRS 模板）：ForgeAI 的章节与之不一定对齐。

## 4. 如何使用

### 4.1 启动一个新项目

```bash
# 1. 把 docs/ 复制到你的新项目仓库
cp -r ForgeAI/docs /path/to/your-new-project/docs
cp ForgeAI/CONTEXT.md /path/to/your-new-project/CONTEXT.md

复制 docs文件夹和CONTEXT.md：
<img width="620" height="148" alt="image" src="https://github.com/user-attachments/assets/ccfe87b6-df94-47f2-847c-0c1d9ab3885f" />

# 2. 在新项目仓库，让 AI 先读取 docs/INIT-GUIDE.md 并按引导补齐占位符
```

### 4.2 日常迭代

进入项目后，所有会话由 `docs/AGENT-GUIDE.md` 协议驱动。每次任务：

1. AI 读取 `README.md` → `AGENT-GUIDE.md` → 任务相关的设计文档。
2. 在 `AGENT-GUIDE.md` 第 8 章登记任务 ID（`XX-NNNN`，XX 为项目缩写）。
3. 实现、测试、文档同步更新。
4. 收尾按 AGENT-GUIDE 第 6 章执行。

## 5. 文件清单

| 路径 | 作用 |
| --- | --- |
| `README.md` | 本文件：ForgeAI 自述与使用说明 |
| `CONTEXT.md` | 新项目的领域术语表、业务上下文、角色与边界 |
| `docs/README.md` | 新项目的文档总览与导航 |
| `docs/AGENT-GUIDE.md` | AI 会话协议与任务台账 |
| `docs/INIT-GUIDE.md` | 新项目初始化问题清单与填充映射 |
| `docs/00~17` | 18 份编号化设计文档骨架（需求 → 架构 → 领域 → 数据 → API → 横切 → 前端 → 规范 → 部署 → 测试 → RoadMap） |
| `docs/18-云服务器生产部署手册(模板).md` | 生产 Runbook 骨架（备份/发布/回滚/冒烟/清理） |
| `docs/模块设计/` | 核心业务模块文档模板与使用说明 |
| `docs/adr/` | 架构决策记录（ADR）模板与示例 |
| `docs/agents/` | Agent 工具链约定（issue-tracker、triage-labels、domain） |

## 6. 核心约定

- 所有 Markdown 文件使用 **UTF-8 with BOM + CRLF** 行尾。
- 编号 `00-17` 为稳定主干；`18` 是生产 Runbook；核心业务模块文档统一放 `docs/模块设计/`。
- 需求编号 `FR-*`、非功能需求 `NFR-*`、领域规则 `DR-*`、架构决策 `ADR-*`。
- 任务 ID `XX-NNNN`，XX 为项目缩写（2-4 字母，大写），在 `INIT-GUIDE` 第 ① 步确定。
- 技术栈的单一事实来源为 `docs/03-系统架构设计(SAD).md` §2，其他文档必须引用它，禁止散落。
- 衍生项目不应残留 `ForgeAI` 字样；根 `README.md` 不复制到新项目。

## 7. 维护与演进

- ForgeAI 作为模板本体，升级后不自动同步到已衍生的项目。
- 新项目遇到 ForgeAI 不覆盖的通用模式时，先在该项目落地并稳定运行；回流 ForgeAI 时提炼为中立骨架。
- 骨架内不保留具体业务示例（避免误用），示例以 ADR 或 CHANGELOG 的方式单独维护。

## 8. 变更记录

| 版本 | 日期 | 变更说明 |
| --- | --- | --- |
| 0.1.0 | 2026-10-15 | 初始骨架：00-17 文档模板 + 18 生产 Runbook + AGENT-GUIDE + INIT-GUIDE + CONTEXT + 模块设计 + ADR + agents |
