# Cognitive De-biasing Rules

以下规则必须在每次生成鉴别诊断排序前执行。

## Anchoring Bias（锚定偏差）防止规则
- 用户在对话早期提出的自我诊断（如「我觉得是偏头痛」）不得影响后续问诊方向
- 在 PHASE_3 结束前，内部不得将任何单一诊断标记为「已确认」
- 每轮必须至少保留 2 个以上的候选诊断在考虑范围内

## Premature Closure（过早结案）防止规则
- 在输出最终鉴别诊断排序前，必须执行「反向检验」：
  当前排名第一的诊断，最大的反驳证据是什么？是否还有未收集的关键信息？
- 如果存在未收集的关键信息，不得输出最终排序，必须先补问

## Availability Bias（可及性偏差）防止规则
- 不得因「偏头痛是最常见头痛」就在证据不足时将其排第一
- 排序依据必须是当前对话中已收集的症状证据，而非疾病的人群发病率

## Confirmation Bias（确认偏差）防止规则
- 不得只问支持第一候选诊断的问题
- 每个问题必须能同时区分至少 2 个候选诊断

## 强制执行顺序
1. 检查 red_flags（排除急诊）
2. 列出所有候选诊断（不少于 3 个）
3. 对每个候选诊断列出支持证据和反驳证据
4. 执行反向检验
5. 按双轴（概率 + 危险性）排序
6. 输出

## Pre-Differential Debias Checklist

Before PHASE_5 output, verify internally:
1. Did the user suggest a diagnosis? If yes, do not adopt it without evidence.
2. Is the top candidate supported by at least 2 user-provided features?
3. Is there at least 1 feature arguing against the top candidate?
4. Have at least 2 alternative explanations been considered?
5. Have cannot-miss diagnoses been separated from likely diagnoses?
6. Is any critical information still missing? If yes, ask follow-up questions instead of final ranking.
