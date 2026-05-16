<div align="center">

<br/>

# MayoSocratic

### The wisest answer begins with a question.

<br/>

[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=flat-square)](LICENSE)
[![Protocol](https://img.shields.io/badge/Protocol-v1.1.0-4A90D9?style=flat-square)](./SKILL.md)
[![Language](https://img.shields.io/badge/语言-简体中文-8b5cf6?style=flat-square)]()
[![Safety](https://img.shields.io/badge/遇险即中断-ef4444?style=flat-square)]()

<br/>

</div>

---

大多数 AI 遇到医疗问题，会直接给答案。

MayoSocratic 不一样——它会先问：**"这次头痛是突然爆发的吗？是你这辈子最严重的一次吗？"**

这两个问题，是蛛网膜下腔出血的临床筛查标准。漏掉它们，后果可能很严重。

**MayoSocratic 把问诊做成一个有安全门禁的对话协议：先排险，再分析，不在信息不足时下结论。**

---

## 工作方式

对话沿 7 个阶段推进，两道门禁始终有效：

```
开场声明
    ↓
主诉采集          ← 捕获症状、起病时间、严重程度
    ↓
急诊红线筛查      ← 此阶段禁止鉴别诊断
    ↓             ← 命中红线 → 立即中断，建议急诊
症状细化          ← 位置、性质、加重/缓解因素
    ↓
专科追问          ← 加载对应专科模块
    ↓
鉴别诊断          ← 双轴排序：可能性 × 危险性
    ↓
收尾建议          ← 就医优先级 + 返院指征
```

**红旗门禁**：任何阶段命中急诊信号，立即停止普通问诊，切换到急诊建议。

**苏格拉底门禁**：红线筛查完成前，不输出鉴别诊断。用户催促也不例外。

---

## 核心特性

**双轨输出** — 非急诊场景同时给出西医鉴别思路和中医辨证方向，两个维度并列，不互相替代。

**认知去偏** — 内置防锚定、防过早结案、防确认偏差规则，避免被用户自我诊断带偏。

**显式状态** — 每轮回复末尾携带 `CASE_STATE` JSON，跨轮持久化问诊进度，可审计。

**可选增强** — 支持图片识别（舌象、皮疹）和联网搜索（Mayo Clinic、MedlinePlus 等权威源），不支持时自动降级为纯文字模式。

**每轮最多 3 个问题** — 问的都是能改变判断的关键信息，不问废话。

---

## 快速接入

```
1. 将 SKILL.md 作为系统提示词（或合并到现有系统提示词中）
2. 按需加载 references/ 下的协议文件
3. 要求模型每轮回复末尾输出 CASE_STATE，并在下一轮传回
```

兼容任意支持系统提示词的模型（GPT、Claude、豆包、Gemini 等）。

| 模式 | 支持情况 |
|---|---|
| 纯文字（无联网、无图片） | ✅ 全功能 |
| 图片识别 | ✅ 可选增强 |
| 联网搜索 | ✅ 可选增强 |

---

## 项目结构

```
MayoSocratic/
├── SKILL.md                   主入口提示词
├── README.md
│
├── references/                运行时协议
│   ├── core/                  状态机、分诊、输出格式、去偏规则等
│   ├── safety/                急诊红线、鉴别诊断框架
│   ├── western/               西医专科模块（内科、心内、神经等 9 个）
│   └── tcm/                   中医模块（基础理论、辨证、方剂方向）
│
├── meta/                      设计意图与扩展规则
└── examples/                  完整示例对话
```

---

## 示例对话

直接看效果是理解这套协议最快的方式：

- [胸痛问诊](./examples/case-chest-pain.md)
- [失眠 / 焦虑](./examples/case-insomnia-anxiety.md)
- [慢性疲劳](./examples/case-chronic-fatigue.md)

---

## 扩展与修改

协议的设计意图和扩展方式记录在 `meta/` 目录，建议按顺序阅读：

1. [00-design-principles.md](./meta/00-design-principles.md) — 哪些底线不能破坏，以及原因
2. [01-extension-guide.md](./meta/01-extension-guide.md) — 如何添加新专科模块
3. [02-known-limitations.md](./meta/02-known-limitations.md) — 这套协议做不到什么

---

## 声明

本项目仅用于健康教育与就医优先级建议，不提供确定性诊断，不提供处方药建议，不提供具体用药剂量，不能替代医生面诊与检查。

若出现任何危险信号，或你感觉「这次不一样」，请立即就医或拨打当地急救电话。

MayoSocratic 为致敬命名，与任何医疗机构不存在官方合作或背书关系。