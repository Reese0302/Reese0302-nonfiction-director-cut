# Blue Book Reference Checklist

## Status

```text
Status: Supplemental validation asset
Authority: Secondary to validation/validation-checklist.md
Applies to: Future maintenance and Phase 4 candidates
Does not apply to: Current frozen migration acceptance
```

## Purpose

This checklist verifies whether future changes to the Director's Cut Skill system remain aligned with the six adopted Blue Book reference principles documented in `migration/blue-book-reference-map.md`.

It does **not** replace `validation/validation-checklist.md` and does **not** introduce new format requirements.

本文件不改变当前冻结结构。本文件不替代 `validation/validation-checklist.md`。本文件只用于后续修改、维护、复盘时检查是否仍符合 `blue-book-reference-map.md` 中采纳的六项设计原则。

## Scope

**Applies when:**
- Modifying `SKILL.md`
- Adding or changing files under `specs/`
- Adding or changing files under `templates/`
- Modifying validation logic
- Introducing new maintenance or iteration documents
- Preparing a post-change review

**Does not apply to:**
- Normal daily usage
- One-off output generation
- External Blue Book format conversion
- Agent Skills Hub distribution work

---

## 1. Progressive Loading

入口轻、模块细、资源后置。

- [ ] `SKILL.md` remains a lightweight routing and control entry. New detailed rules are placed in the appropriate module, not directly accumulated in `SKILL.md`.
- [ ] Templates are only invoked when output structure is needed, not loaded unconditionally.
- [ ] Validation assets are not loaded as execution instructions unless a review or test is being performed.
- [ ] No new rule forces all modules to be read for every task. Module loading remains step-conditional.

---

## 2. Agent-Centric Design

写给 Agent 执行的规则，不是写给人类欣赏的说明。

- [ ] Each modified module clearly states when it should be used (触发条件) and when it should NOT be used (非触发条件).
- [ ] Each modified module gives the Agent actionable rules (决策树/条件判断), not only conceptual explanation (散文/综述).
- [ ] `MUST` / `不得` / `禁止` language remains clear and consistent. Vague terms like `按需使用` or `综合考虑` are avoided.
- [ ] Conflict resolution rules remain explicit when multiple modules could apply.

---

## 3. Atomic Module Boundaries

一个模块一个职责，边界不糊。

- [ ] Each new rule belongs to exactly one primary module. Cross-references are used instead of duplicating the same rule in multiple modules.
- [ ] No module silently absorbs unrelated responsibilities. Each module's "模块职责" section accurately reflects its current scope.
- [ ] Any module approaching 15KB is reviewed for possible splitting. No module exceeds 20KB without explicit justification.
- [ ] `SKILL.md` is not used as a dumping ground for unresolved policy decisions.

---

## 4. Iteration Loop

基于真实错误驱动，不凭感觉改。

- [ ] Every substantive rule change is linked to a real issue, observed failure, or approved design decision. No "心血来潮" changes.
- [ ] Proposed changes distinguish between one-off edge cases and recurring system-level issues. Edge cases do not become permanent rules unless they recur.
- [ ] Each modification removes at least 1 line of obsolete content OR fixes 1 specific bug. No "add only" commits.
- [ ] If `validation/mistakes-log.md` exists, relevant entries are updated before or during the change.
- [ ] The change does not erase historical migration rationale recorded in `migration/monolith-baseline-map.md`.

---

## 5. Validation-First Maintenance

先验收，再冻结。

- [ ] The primary `validation/validation-checklist.md` (22 items) is still passed after the change.
- [ ] The change does not introduce unresolved terminology drift. Key terms (案例等级: 证据型/例子型/类比型; 素材类型: 非虚构书/长文章/系列内容/文集型; 模式: Quick/Standard/Deep) remain consistent with their authoritative definitions in `specs/`.
- [ ] The change does not expose internal module paths in normal user-facing responses, except in debugging, stress-testing, or specification maintenance contexts.
- [ ] The change has been reviewed against at least one realistic usage scenario from the 9-scenario stress test suite.

### 5.1 Recorded Optimization Notes

The following five items were recorded in the Phase 3 freeze and are re-stated here as maintenance guardrails. Each should be checked when modifying relevant modules.

- [ ] **响应简洁**: 真实用户响应中减少内部模块路径暴露。压测、调试、规范维护场景除外。
- [ ] **术语统一 — 片段型素材**: 片段型素材统一表述为"局部 Standard"，避免误解为全书级 Standard。
- [ ] **术语统一 — 案例等级**: 案例等级术语统一使用 `specs/case-policy.md` 正式名称：证据型 / 例子型 / 类比型。正文中不得出现等级标签，降调时用自然语言表达。
- [ ] **中文场景标注**: 中文场景转换时明确标注为"语境补充"，使用"换成中文读者更熟悉的场景……"等提示语，避免被误读为原书内容。
- [ ] **案例表述克制**: 现实案例表述避免戏剧化和过度定性。优先使用稳健、公共现象级表达（如"变化"而非"骤停"）。

---

## 6. Obsolescence and Maintenance Risk

保持呼吸信号，不悄悄腐烂。

- [ ] The last review date is recorded when a meaningful maintenance pass is completed.
- [ ] A 90-day review signal is maintained for core policy modules. At minimum, `validation/mistakes-log.md` (if created) is touched within each 90-day window.
- [ ] Known limitations are not hidden or overwritten. If a limitation is discovered, it is recorded before being fixed.
- [ ] Changes caused by external context shifts (Claude behavior change, tool capability change, upstream format change) are marked as such in the change record.
- [ ] Frozen baseline files (`migration/monolith-baseline-map.md`, `migration/blue-book-reference-map.md`) remain distinguishable from active maintenance files. Baseline files are only updated via explicit migration phases, not ad-hoc edits.

---

## Usage Notes

1. This checklist is invoked **before finalizing** a maintenance change, not during normal Skill execution.
2. Not all items apply to every change. Skip items that are clearly irrelevant, but note the skip reason.
3. If a change intentionally violates a checklist item, document the rationale in the change record.
4. This checklist may be updated as the Blue Book reference map evolves. Changes to this checklist must not contradict the frozen migration baseline.

## Document Metadata

- **Created**: 2026-05-09
- **Parent**: `migration/blue-book-reference-map.md`
- **Peer**: `validation/validation-checklist.md` (primary, higher authority)
- **Lines**: ~170
