# Changelog

本文档记录 `nonfiction-director-cut` 的重要版本变化。

本项目遵循"结构变化可追溯、规则变化需说明、维护变化不伪装成功能变化"的原则。

## 2026-05-09 — v1.0.0

### 完成

- 完成三阶段模块化迁移。
- 将原 monolith `SKILL.md` 拆分为轻量入口与模块化规则文件。
- 将根 `SKILL.md` 转换为蓝皮书式轻量 Skill 入口。
- 完成蓝皮书参考优化层建设。
- 完成迁移残留清理。
- 新增 GitHub 发布所需的基础文档。

### 当前结构

```text
nonfiction-director-cut/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── SKILL.md
├── specs/
├── templates/
├── validation/
└── migration/
```

### 核心文件

- `SKILL.md`：轻量入口，负责触发、核心行为、最小执行流程和模块路由。
- `specs/`：核心规则层，负责来源判断、模式选择、写作规则、案例策略和输出策略。
- `templates/`：模板层，负责触发响应和正文骨架。
- `validation/`：校验与维护层，负责验证清单、蓝皮书参考检查和运行错误记录。
- `migration/`：迁移追溯层，负责迁移基线和方法论映射。

### 迁移与对齐

- 原 `SKILL.md` 已从迁移型总控文档压缩为蓝皮书式轻量入口。
- 根入口保留触发说明、核心行为、优先级规则、执行流程和模块路由。
- 详细规则继续由 `specs/` 承接。
- 模板继续由 `templates/` 承接。
- 校验与维护继续由 `validation/` 承接。
- 迁移追溯继续由 `migration/` 承接。

### 蓝皮书参考层

新增并完成以下辅助维护文件：

- `migration/blue-book-reference-map.md`
- `validation/blue-book-checklist.md`
- `validation/mistakes-log.md`

这些文件只用于方法论映射、后续维护检查和真实错误记录，不直接定义新的执行规则。

### 发布文档

新增：

- `README.md`
- `LICENSE`
- `CHANGELOG.md`

许可证：

- CC BY-NC-SA 4.0
- Copyright (c) 2026 Reese0302

### 清理

- 清理 specs 与 templates 中的迁移期残留表述。
- 将迁移期过渡说明替换为稳定的"来源 + 迁移已完成 + 后续维护来源"说明。
- 将 Phase 4 前备份文件移入本地 `.trash/`，不作为公开发布内容。

### 规则变更

```text
核心规则变更：0
模块边界变更：0
路由变更：0
优先级变更：0
```

本版本主要是结构化、轻量化、发布准备和维护层补齐，不引入新的行为规则。

### 当前状态

```text
三阶段模块化迁移：已完成
蓝皮书参考优化层：已完成
蓝皮书格式对齐：已完成
迁移残留清理：已完成
GitHub 发布准备：进行中
```

## 维护约定

后续版本记录应明确区分以下几类变化：

### Added

新增文件、新增模块、新增模板或新增公开文档。

### Changed

已有规则、入口、模板、流程或权威层级发生变化。

### Fixed

修复真实使用中发现的问题，通常应对应 `validation/mistakes-log.md` 中的记录。

### Removed

删除不再使用的规则、模板、迁移残留或内部文件。

### Documentation

只影响说明文档、README、贡献指南、发布说明等，不改变 Skill 行为。

### Maintenance

只影响清理、归档、格式整理、校验流程或项目卫生，不改变 Skill 行为。
