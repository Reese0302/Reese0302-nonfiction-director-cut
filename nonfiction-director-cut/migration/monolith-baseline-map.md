# Monolith Baseline Map

基准文件：`SKILL.md`

基准状态：结构性重构前最后一版

基准时间：2026-05-09 11:15

版权主体：Reese0302

许可证：MIT

## 迁移状态

本文件同时承担两个角色：

1. **迁移映射表**：记录原 `SKILL.md` 每一块未来要搬到哪里
2. **迁移进度追踪器**：每搬完一块，直接更新表中状态

不额外建 `split-log.md`。所有进度追踪以本表为准。

状态统一使用以下四种：

```text
pending  — 尚未开始
partial — 部分搬完
done    — 已完成
deferred — 暂不搬
```

## 迁移原则

本次结构化重构以语义等价迁移为目标。

第一阶段只调整文件结构，不主动新增业务规则，不改变原 Skill 的核心行为。

所有从 monolith `SKILL.md` 中拆出的规则，都必须能追溯到原文件中的对应章节。

## 目标结构

```text
nonfiction-director-cut/
  SKILL.md

  specs/
    source-and-mode-policy.md
    writing-policy.md
    case-policy.md
    memory-rag-spec.md
    output-policy.md

  templates/
    trigger-response.md
    skeleton-template.md

  validation/
    validation-checklist.md

  migration/
    monolith-baseline-map.md
```

## 迁移映射表

| 原章节 / 原内容 | 目标文件 | 迁移状态 | 备注 |
|---|---|---|---|
| YAML frontmatter：`name` / `description` / `triggers` | `SKILL.md` | pending | 保留在主入口文件中，后续可优化 description，但第一阶段不改语义 |
| v1.1 / v1.2 变更说明 | `SKILL.md` 或后续 `CHANGELOG.md` | pending | 第一阶段可暂留主文件，公开发布前再移入 changelog |
| Skill 总说明：非虚构内容中文导演剪辑版 | `SKILL.md` | pending | 主入口保留简短定位 |
| 最高优先级规则 | `SKILL.md` | pending | 必须保留在主入口，作为全局硬规则 |
| 主 SKILL.md 模块索引与调用原则 | `SKILL.md` | done | 已增加模块化引用说明和调用原则，作为主文件瘦身阶段的入口索引 |
| 主 SKILL.md Step 0/1/3/4 瘦身 | `SKILL.md` | done | 已将 Step 0、Step 1、Step 3、Step 4 的原始长段规则替换为模块引用；详细规则分别由 source-and-mode-policy、writing-policy、case-policy 承接 |
| 主 SKILL.md 剩余后置规则瘦身 | `SKILL.md` | done | 已将 Step 1.6、Step 2/2.5-2.7、Step 4.10、Step 5-11 及边界情况、文件输出、文件命名、验证方式等后置长段规则替换为模块引用 |
| 主 SKILL.md 大段瘦身 | `SKILL.md` | done | 已完成主文件中已迁移长段规则的模块化引用替换；主文件保留总控流程、模块索引和必要调用说明；详细规则由 specs / templates / validation 下的模块文件维护 |
| 全局原则：参考对象抽象化、静默默认、防幻觉、版权原则 | `SKILL.md` + `specs/source-and-mode-policy.md` + `specs/output-policy.md` | pending | 主文件保留核心原则，展开细则按职责拆分 |
| 执行总顺序 | `SKILL.md` | pending | 保留在主入口，作为 Agent 调度总控 |
| Step 0.1 仅触发词输入时的固定回应 | `templates/trigger-response.md` | done | 模板类内容，已迁移；主文件原文暂保留，待后续瘦身时替换为引用 |
| Step 0 入口判断与模式选择 | `specs/source-and-mode-policy.md` | done | 入口职责、触发识别、素材类型判断、用户视角判断、模式判断、版本确认与入口输出全部迁移完成；主文件原文暂保留，待后续瘦身时替换为引用 |
| Step 0.2 用户视角识别 | `specs/source-and-mode-policy.md` | done | 已迁移至 `specs/source-and-mode-policy.md`；父级 Step 0 已完成 |
| Step 0.3 素材类型识别 | `specs/source-and-mode-policy.md` | done | 已迁移至 `specs/source-and-mode-policy.md`；父级 Step 0 已完成 |
| Step 0.4 输入类型识别 | `specs/source-and-mode-policy.md` | done | 已迁移至 `specs/source-and-mode-policy.md`；父级 Step 0 已完成 |
| Step 0.5 模式默认与推荐规则 | `specs/source-and-mode-policy.md` | done | 已迁移至 `specs/source-and-mode-policy.md`；父级 Step 0 已完成 |
| Step 0.6 版本确认 | `specs/source-and-mode-policy.md` | done | 已迁移至 `specs/source-and-mode-policy.md`；父级 Step 0 已完成 |
| Step 1 主问题与机制提取 | `specs/writing-policy.md` | done | 主问题提取、机制识别、主机制与辅助机制、三层解释、避免摘要化、避免过度发挥与机制输出格式已迁移完成 |
| Step 1.1.5 主问题提取按素材类型分化 | `specs/writing-policy.md` + `specs/source-and-mode-policy.md` | done | 内容已拆分迁移至 `specs/writing-policy.md` 与 `specs/source-and-mode-policy.md` |
| Step 1.4 骨架输出模板 | `templates/skeleton-template.md` | done | 模板类内容，已迁移；主文件原文暂保留，待后续瘦身时替换为引用 |
| Step 1.5 Quick 模式骨架规则 | `specs/output-policy.md` 或后续 Quick 模板 | done | 第一阶段先归 output-policy |
| 最终输出、交付形态与限制说明 | `specs/output-policy.md` | done | 输出前置判断、默认输出说明、正式正文输出、中间判断展示、Quick/Standard/Deep 输出边界、限制说明、案例池输出、骨架输出、多版本输出、输出格式与最终检查已迁移完成 |
| 资料读取、记忆调用与 RAG 规则 | `specs/memory-rag-spec.md` | done | 资料来源类型、资料优先级、记忆与 RAG 调用条件、检索转换、检索结果使用、来源归属、冲突处理、素材不足处理与输出前检查已迁移完成 |
| Step 1.6 跨篇观点召回 | `specs/memory-rag-spec.md` | done | 记忆系统完整迁移 |
| Step 2 骨架持久化 | `specs/output-policy.md` | done | 属于交付与文件持久化规则 |
| Step 2.5 双层观点记忆 RAG | `specs/memory-rag-spec.md` | done | 记忆系统完整迁移 |
| Step 2.6 观点记忆调入流程 | `specs/memory-rag-spec.md` | done | 记忆系统完整迁移 |
| Step 2.7 观点记忆文件模板 | `specs/memory-rag-spec.md` | done | 第一阶段先放 memory spec，后续可再拆模板 |
| Step 3 案例搜索与案例池 | `specs/case-policy.md` | done | 案例功能、本土化、案例池、案例等级、搜索规则、案例禁区、搜索预算、搜索失败降级、证据剪裁全部迁移完成；主文件原文暂保留，待后续瘦身时替换为引用 |
| Step 4 正文写作与表达规则 | `specs/writing-policy.md` | done | 正文主线、开头写法、概念解释、机制写法、原文证据、现实案例、段落组织、过渡转折、语言风格、忠实转译、结尾写法与正文生成前检查已迁移完成 |
| Step 4.10 成稿控制：机制、案例与行动建议 | `specs/writing-policy.md` + `specs/case-policy.md` + `specs/output-policy.md` | done | 机制缺口归 writing，案例控制归 case，交付边界归 output |
| Step 5 以后与输出模式相关内容 | `specs/output-policy.md` | done | 具体以原文后半部分为准 |
| Step 9 输出前自检 / 验证规则 | `validation/validation-checklist.md` | done | 自检清单与 Quick / Standard / Deep 验证方式已迁移；主文件原文暂保留，待后续瘦身时替换为引用 |
| Step 11 局部重写 / 回流机制 | `specs/output-policy.md` | done | 第一阶段先归 output-policy，后续可单独拆 `local-rewrite-policy.md` |
| 版权说明模板 | `specs/output-policy.md` | done | 最终输出规则 |
| 文件命名、分段输出、交付规则 | `specs/output-policy.md` | done | 输出层规则 |
| 运行时记忆目录说明 | `specs/memory-rag-spec.md` | done | 先放记忆规范，不提交真实运行数据 |
| 案例池模板 | `specs/case-policy.md` | deferred | 案例池模板暂不纳入第一阶段语义等价迁移；后续阶段如需独立模板再处理 |
| 所有内部字段禁止进入正文的规则 | `SKILL.md` + `validation/validation-checklist.md` | done | 规则已拆分至主 `SKILL.md` 调用说明与 `validation/validation-checklist.md` |
| 第三阶段第一轮：静态一致性校验 | `SKILL.md` + 全部模块文件 | done | 主文件职责、模块路径、职责边界、迁移地图闭合、Step 调用链全部通过；修正 4 处迁移地图状态 |
| 第三阶段第二轮：典型任务调用压测 | `SKILL.md` + specs/templates/validation | done | 已完成 9 个典型任务压测；主文件总控入口与各模块调用链验证通过，发现 5 处非阻塞优化项 |

## 第一阶段不处理的事项

第一阶段暂不处理以下事项：

1. 不重写核心业务规则。
2. 不新增新的输出模式。
3. 不新增复杂目录。
4. 不单独拆 `docs/`、`examples/`、`scripts/`。
5. 不改动 MIT 许可证内容。
6. 不提交真实用户数据、原文资料、生成稿、记忆卡或案例池运行文件。

## 第一阶段完成标准

第一阶段完成时，应满足：

1. `SKILL.md` 仍然可以作为主入口使用。
2. 原 monolith 中的主要规则都有明确迁移目标。
3. 每个拆分文件的职责清楚，不互相抢规则。
4. 没有因为拆分导致规则语义变化。
5. 后续可以按本表逐块迁移内容。

## 第三阶段记录

### 第一轮：静态一致性校验

结果：通过。

检查项：
- 主 SKILL.md 已只保留总控流程、模块索引和短引用。
- 模块路径全部指向目标结构内文件，未发现 `problem-and-mechanism-policy.md` / `structure-policy.md` 残留。
- 各模块职责边界清晰，未发现明显重复维护。
- Step 调用链可读通。
- 迁移地图中 Step 0.2-0.6 子行、Step 1.1.5、内部字段禁止进入正文改为 done；案例池模板改为 deferred。

可选修订（暂不处理）：8 个模块末尾迁移说明中"待后续主文件瘦身时替换"表述已过时。

### 第二轮：典型任务调用压测

结果：通过。

已完成 9 个典型场景：

| 场景 | 输入特征 | 预期模块 | 结果 |
|---|---|---|---|
| 1 | 只有书名 | source-and-mode + memory-rag + output | 通过 |
| 2 | 提供片段 | source-and-mode + writing + output | 通过 |
| 3 | 提供全文 | source-and-mode + writing + output | 通过 |
| 4 | 要求中文读者版 | source-and-mode + writing + case + output | 通过 |
| 5 | 要求 Deep 但素材不足 | source-and-mode + memory-rag + output | 通过 |
| 6 | 要求只迁移文件 | source-and-mode + memory-rag + output | 通过 |
| 7 | 要求先看骨架 | source-and-mode + writing + skeleton-template + output | 通过 |
| 8 | 要求案例池 | source-and-mode + writing + case-policy + output | 通过 |
| 9 | 要求最终成稿 | source-and-mode + writing + skeleton + case + output + validation | 通过 |

结论：主 `SKILL.md` 已能作为轻量总控入口使用；入口判断、资料边界、写作政策、案例政策、骨架模板、输出政策和质量校验均能按任务类型正确调用。

轻微优化项（非阻塞，记录备后续）：

1. 真实用户响应中减少内部模块路径暴露。
2. 片段型素材建议统一表述为"局部 Standard"。
3. 案例等级字段需与 `specs/case-policy.md` 正式等级定义保持一致。
4. 中文场景转换应更明确标注为"语境补充"。
5. 现实案例表述应避免戏剧化和过度定性（如"骤停"→"变化"）。

## 第三阶段第三轮：修复记录与最终冻结

结果：冻结。

第一、二阶段已完成全部模块化迁移和主文件瘦身。

第三阶段已完成静态一致性校验和 9 场景调用压测。

五项轻微优化项全部记录为后续使用注意事项，本轮不做文件修改：

1. 真实用户响应减少内部模块路径暴露；压测、调试、规范维护场景除外。
2. 片段型素材建议统一表述为"局部 Standard"，避免误解为全书级 Standard。
3. 案例等级术语统一使用 `specs/case-policy.md` 正式名称：证据型 / 例子型 / 类比型。
4. 中文场景转换时，建议使用"换成中文读者更熟悉的场景……"等提示语，明确其属于语境补充。
5. 现实案例表述应避免戏剧化和过度定性，优先使用稳健、公共现象级表达。

### 最终状态

- 主 `SKILL.md`：442 行，已瘦身为轻量总控入口。
- 模块文件：8 个，包含 `specs` × 5、`templates` × 2、`validation` × 1。
- 迁移地图：所有模块迁移 `done`，主文件瘦身 `done`，第三阶段静态校验与调用压测 `done`。
- 语义等价：全程未新增规则、未改变优先级、未改变默认流程。
- 文件结构：未新增未经确认的目标文件名，已按原迁移映射表完成。
- 后续维护：详细规则由模块文件维护，主 `SKILL.md` 只保留总控流程、模块索引和必要调用说明。

迁移完成。

本项目三阶段模块化迁移正式冻结。
