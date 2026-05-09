# nonfiction-director-cut

`nonfiction-director-cut` 是一个用于非虚构内容中文改写与深度解读的模块化 Skill。

它的目标不是把一本书、一篇长文或一组材料机械总结成读书笔记，而是提炼素材真正想回答的主问题，重组其中的核心机制，并把它改写成一篇中文读者更容易读懂、愿意读完、读完有安顿感的"导演剪辑版"文章。

## 它能做什么

这个 Skill 适用于以下非虚构内容：

- 非虚构书
- 长文章
- 系列文章
- 文集型材料
- 片段型材料
- 需要面向中文读者重讲的复杂内容

它会重点处理：

- 主问题提炼
- 核心机制识别
- 问题链重组
- 中文语境解释
- 案例选择与本土化判断
- 成稿结构控制
- 输出前质量校验

最终输出应当像一篇连续文章，而不是章节摘要、资料卡片、课程提纲或内部分析报告。

## 它不适合做什么

这个 Skill 不适合用于：

- 小说改写
- 纯翻译
- 逐章复述
- 金句摘抄
- 普通读书笔记
- 学术文献综述
- 热点评论
- 营销文案
- 无依据的案例编造
- 将所有外国案例机械替换成中文案例

本土化不是"把外国例子一律换成中国例子"，而是在不扭曲原素材机制的前提下，降低中文读者的理解成本。

## 典型触发方式

可以使用以下触发词或自然语言请求：

```text
/director-cut
/book-localize
/非虚构导演剪辑版
/中文导演剪辑版
/导演剪辑版
/长文导演剪辑版
/推文导演剪辑版
非虚构书中文导演剪辑版
用中文语境重讲这本书
这本书的核心问题
这本书讲了什么
用导演剪辑版重写这篇文章
替换书中例子
```

## 安装

```bash
npx skills add Reese0302/nonfiction-director-cut
```

或手动安装：

```bash
git clone https://github.com/Reese0302/nonfiction-director-cut.git
cp -r nonfiction-director-cut ~/.claude/skills/
```

## 基本使用方式

你可以提供以下任意一种材料：

- 书名
- 书籍目录
- 书籍摘录
- 文章全文
- 文章链接内容
- 系列文章材料
- 你的阅读笔记
- 已整理的素材包

然后提出类似请求：

```text
用导演剪辑版重讲这本书。
```

或者：

```text
请把这篇长文改写成中文读者更容易理解的导演剪辑版。
```

如果素材不足，Skill 会输出局部版本、限制说明，或要求补充必要信息。它不会在信息不足时伪装成完整判断。

## 输出模式

Skill 支持多种输出模式。

`Quick` 模式用于快速判断"值不值得读、应该怎么读"。它不是 Standard 的缩短版，而是一个决策层输出。

`Standard` 模式用于生成完整的导演剪辑版文章。

`Standard Plus` 模式用于在 Standard 基础上加强解释密度。

`Deep` 模式用于更深入的机制重建、语境处理和案例判断。

## 读者视角与创作者视角

默认采用读者视角。

读者视角会直接面向最终读者输出成稿，减少内部过程展示。

当用户表现出发布、编辑、写稿、脚本、选题、结构设计等意图时，会进入创作者视角。创作者视角可以先输出骨架、结构方案、案例池或分段确认内容。

## 项目结构

```text
nonfiction-director-cut/
├── SKILL.md
├── specs/
├── templates/
├── validation/
└── migration/
```

`SKILL.md` 是蓝皮书式轻量入口，负责触发说明、核心行为、最小执行流程和模块路由。

`specs/` 是核心规则层，负责来源判断、模式选择、写作规则、案例策略和输出策略。

`templates/` 是模板层，负责触发响应和正文骨架等可复用结构。

`validation/` 是校验与维护层，负责主验证清单、蓝皮书参考检查和运行错误记录。

`migration/` 是迁移追溯层，记录模块化迁移过程、蓝皮书参考映射和历史基线。

## 文件说明

```text
SKILL.md
```

根入口文件。保持轻量，只承担触发、总控、优先级和模块加载说明。

```text
specs/source-and-mode-policy.md
```

负责素材类型、用户视角、输出模式、触发判断和版本确认。

```text
specs/memory-rag-spec.md
```

负责资料边界、记忆调用、RAG 检索、来源优先级和归属判断。

```text
specs/writing-policy.md
```

负责主问题提取、机制识别、正文写作、三层解释和表达规则。

```text
specs/case-policy.md
```

负责案例搜索、本土化、案例等级、案例禁区和证据剪裁。

```text
specs/output-policy.md
```

负责最终交付形态、限制声明、版权说明、中间判断展示和输出边界。

```text
templates/trigger-response.md
```

负责触发后的简短响应模板。

```text
templates/skeleton-template.md
```

负责导演剪辑版正文骨架模板。

```text
validation/validation-checklist.md
```

主验证清单，用于检查输出质量、规则一致性和迁移后的语义等价。

```text
validation/blue-book-checklist.md
```

蓝皮书参考维护清单，用于后续修改时检查是否破坏渐进加载、Agent 视角、模块原子化等原则。

```text
validation/mistakes-log.md
```

运行证据日志，用于记录真实使用中的错误、偏差和反复出现的问题。它不直接定义新规则。

```text
migration/monolith-baseline-map.md
```

原 monolith 迁移基线，用于追踪原规则迁移到哪个模块。

```text
migration/blue-book-reference-map.md
```

蓝皮书参考映射，用于说明哪些思想被采纳、哪些不采纳，以及如何映射到当前系统。

## 规则权威层级

当文件之间出现冲突时，建议按以下顺序判断：

1. `SKILL.md`
2. `specs/`
3. `templates/`
4. `validation/validation-checklist.md`
5. `migration/monolith-baseline-map.md`
6. 蓝皮书参考文件与维护日志

其中，`validation/mistakes-log.md` 只记录证据，不直接定义规则。

## 当前状态

```text
三阶段模块化迁移：已完成
蓝皮书参考优化层：已完成
蓝皮书格式对齐：已完成
迁移残留清理：已完成
当前根入口：蓝皮书式轻量 SKILL.md
核心规则变更：0
模块边界变更：0
路由变更：0
```

## 维护原则

后续维护时，建议遵守以下原则：

- 不要把详细规则重新塞回 `SKILL.md`
- 新规则应放入对应的 `specs/` 文件
- 可复用输出结构应放入 `templates/`
- 校验与维护信息应放入 `validation/`
- 迁移记录和历史追溯应放入 `migration/`
- 真实错误应先记录到 `validation/mistakes-log.md`
- 不要因为一次偶发输出问题立刻修改核心规则

## 版权与素材说明

本仓库只包含 Skill 指令、规则、模板、校验清单和迁移说明。

本仓库不包含任何未授权书籍全文、文章全文、用户材料或付费内容摘录。

使用本 Skill 处理具体书籍、文章或其他材料时，请遵守相应内容的版权要求。对于原书或原文内容，应尽量转述，避免大段复制。

## License

See `LICENSE`.
