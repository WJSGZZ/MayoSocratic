# 扩展指南

添加新专科模块、新主诉或新能力时，请按本指南操作。
扩展前请先阅读 meta/00-design-principles.md。

---

## 添加新西医专科模块

按以下顺序执行，不要跳步：

### Step 1：确定文件名

在 references/western/ 中，按现有编号顺序分配新编号。
当前最大编号为 08，新模块命名为 09-[specialty-name].md。

### Step 2：补急诊红旗

在 references/safety/00-emergency-flags.md 中新增该主诉的专项红旗章节。

格式参考：

## [主诉名]专项红旗
- [红旗 1]
- [红旗 2]

### Step 3：补分诊阈值

在 references/core/01-triage.md 中新增该主诉的人群阈值调整（如适用）。

### Step 4：新建专科追问文件

新建 references/western/0X-[specialty].md，参考 references/western/02-neurology.md 的结构：
- 进入条件（什么主诉触发此模块）
- 第一轮问题（PHASE_3 起始，≤3 个）
- 第二轮问题（PHASE_4 专科深化，≤3 个）
- 第三轮问题（背景信息，≤3 个）
- 重要鉴别问题

### Step 5：补 Illness Scripts

在 references/safety/01-differential.md 中新增该主诉的疾病脚本。
每个疾病必须包含完整的 Illness Script 结构（见该文件格式说明）。

### Step 6：补中医证型

在 references/tcm/01-diagnostics.md 中新增该主诉对应的中医证型。

### Step 7：更新 SKILL.md

在 Module Loading Order 的专科路由表中新增该主诉到新模块的映射。

### Step 8：补 examples

在 examples/ 中新增至少一个完整对话案例，展示：
- 红旗筛查
- 专科追问
- 最终双轨输出（西医分析 + 中医辨证分析）

---

## 添加新中医证型

在 references/tcm/01-diagnostics.md 中按以下格式新增：

### [证型名称]
- 典型表现：
- 舌象：舌[色]，苔[色][质]
- 寒热：偏[寒/热/不明显]
- 情志：
- 治法：
- 参考方剂类别：
- 调养建议：

---

## 更新权威搜索源

在 references/core/07-search-protocol.md 的权威源列表中按类别新增。
新增时注明：来源类型、适用场景。

---

## 禁止做的事

- 不要修改急诊中断器的触发逻辑（设计原则一）
- 不要放宽鉴别诊断排序门禁的解锁条件（设计原则二）
- 不要在 PHASE_2 的回复模板中加入任何疾病名称（设计原则四）
- 不要在中医输出里给出具体药物剂量
- 不要声称与 Mayo Clinic 官方有关联（设计原则七）
