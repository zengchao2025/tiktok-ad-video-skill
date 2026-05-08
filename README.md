# TikTok Ad Video Skill

> **面向 TikTok 广告投放场景的 Prompt 自动生成系统**  
> 集成创意搜索、结构评分、NoPost 直发优化与双门控审查机制

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Stars](https://img.shields.io/github/stars/qq547820639/tiktok-ad-video-skill)](https://github.com/qq547820639/tiktok-ad-video-skill/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/qq547820639/tiktok-ad-video-skill)](https://github.com/qq547820639/tiktok-ad-video-skill/forks)

---

## ⚡ 项目简介

**TikTok Ad Video Skill** 是一套完整的 Prompt 自动生成与质量评估系统，专为 TikTok 广告投放团队设计。系统可自动生成可直接投放的视频 Prompt、标题文案、标签、评论及 Bio，同时提供结构质量评分、情绪影响分析、渲染置信度评估以及合规性审查报告，帮助增长团队高效、规模化地生产低后期依赖的广告素材。

本仓库包含 **HappyHorse CreativeOS** 的完整实现体系，由双层架构组成：

- **理论内核** — 《HappyHorse CreativeOS v2.0.1 系统规范定稿》：负责 Prompt 生成、Q1–Q8 评分、CreativeScore、PRC、EAD、NoPostGate、PostReady、VEL、ShowDontTell、审计与修复。
- **执行手册** — 《HappyHorse CreativeOS v2.1-MVP 表格落地版》：负责 9 张表、18 个核心视图、Pilot 执行指南、Decision Dashboard、CalibrationLog 与 Pilot Run Report。

---

## 🏗️ 系统架构

HappyHorse CreativeOS 采用 **双层架构**，严格区分理论与执行：

| 层级 | 文档 | 职责 |
|------|------|------|
| **第一层：理论内核** | HappyHorse CreativeOS v2.0.1 — 系统规范定稿 | Prompt 生成、Q1–Q8 评分、CreativeScore、PRC、EAD、NoPostGate、PostReady、VEL 植入、ShowDontTell 检查、低分诊断、候选 Winner 选择、风险声明、审计检阅 |
| **第二层：执行手册** | HappyHorse CreativeOS v2.1-MVP — 表格落地版 | 9 张表、18 个核心视图、Pilot 执行指南、Decision Dashboard、CalibrationLog、Pilot Run Report |

**核心原则：**
- v2.0.1 负责判断「怎么生成和评分」
- v2.1-MVP 负责规定「怎么记录和执行」
- DeepSeek（或任意 LLM）每次只执行当前 P 步骤，不允许自由发挥

---

## 🧠 核心概念

### 视觉增强层 (VEL)

一个统一的增强词库，分为 **物理真实、角色生命、材质光影、大气粒子** 四大类。在生成 Prompt 时，系统会自动遵循 **分散、不堆叠** 的植入规则（每 Prompt 3–4 个词，每句最多 1 个后缀），以提升画面的视觉表现力，且不会对评分产生负面影响。

### 双门控审查机制

模拟生产管线的质量关卡：

- **NoPostGate** — 检查内容是否满足「无需后期制作即可发布」的直发标准
- **PostReady** — 评估作品是否已达到可投放的专业质量

只有通过双门控审查的内容，才会被视为可交付。

### 评分体系

所有权重均基于 **专家先验** 设定，用于估算创意与结构的质量。**本项目并非投放效果预测模型**，所有权重有待数据校准。VEL 增强词对评分的影响为中性至微幅正面。

---

## 📁 仓库结构

```
tiktok-ad-video-skill/
├── README.md                                          # 本文件
├── HappyHorse CreativeOS v2.0.1 — 系统规范定稿         # 理论内核（第一层）
├── HappyHorse CreativeOS v2.1-MVP — 表格落地版         # 执行手册（第二层）
└── Seedance.md                                        # Seedance 2.0 独立系统 (v3.5)
```

---

## 🚀 快速开始：总控 Prompt

### 第一步：发送总控系统指令

将以下内容作为 System Prompt 发送给 LLM：

```
你现在作为 HappyHorse CreativeOS 的执行代理工作。

你有两份上位文档：
1.《HappyHorse CreativeOS v2.0.1 系统规范定稿》：理论内核，用于 Prompt 生成、Q1-Q8 评分、CreativeScore、PRC、EAD、NoPostGate、PostReady、VEL、ShowDontTell、审计与修复。
2.《HappyHorse CreativeOS v2.1-MVP 表格落地版》：执行手册，用于 9 张表、18 个核心视图、Pilot 执行指南、Decision Dashboard、CalibrationLog 与 Pilot Run Report。

工作原则：
- 当前默认阶段是 v2.1-MVP Pilot Run。
- 不再扩展理论模块。
- 不修改 9 张表主干。
- 不修改 18 个核心视图主干。
- 所有评分是专家先验，不是投放效果预测。
- 只有接入真实生成数据和投放数据并完成校准后，才允许讨论预测关系。
- RenderResult 只记录聚合后的最终标注结果，第一手标注必须进入 Annotation Table。
- Pilot 只有 9 条视频，只验证流程闭环，不满足 Level 1。
- 输出必须能直接填写进表格、执行、追溯。

请先读取我接下来粘贴的两份文档，建立上下文。
读取后只回复：
"已建立 HappyHorse CreativeOS 工作上下文。当前默认阶段：v2.1-MVP Pilot Run。"

不要总结，不要扩展理论。
```

### 第二步：按顺序粘贴两份文档

```
〖文档 1〗 HappyHorse CreativeOS v2.0.1 系统规范定稿
……

〖文档 2〗 HappyHorse CreativeOS v2.1-MVP 表格落地版
……
```

### 第三步：发送当前任务

```
请基于以上两份文档，进入 v2.1-MVP Pilot Run。
现在先执行 P-01 至 P-05：建表、建视图、配权限、选择 3 个产品、准备产品图。

请输出可直接执行的操作清单和需要填写的表格内容模板。
不要扩展理论，不要修改表结构。
```

### 文档投喂策略

| 场景 | 建议 |
|------|------|
| 第一次对话 | 投喂 sys 级总指令 + v2.0.1 + v2.1-MVP 全文，建立上下文 |
| 同一对话后续 | 只发当前任务 + 必要产品信息 |
| 新开对话 | 重新投喂 sys 级总指令 + 两份文档（或至少相关章节） |

---

## 📋 分阶段工作流

### 第 1 步：启动上下文
发送总控 Prompt，让 LLM 读取两份文档并回复确认，避免一上来长篇复述。

### 第 2 步：执行 P-01 至 P-05（建表与产品选择）
建 9 张表、18 个核心视图、角色权限配置、Pilot 产品选择。

### 第 3 步：执行 P-06 至 P-12（Prompt 生成与评分）
为每个产品生成 A/B/C 三个候选（StrongHook / EmotionReversal / ProductFunction），调用 v2.0.1 评分内核进行 Q1–Q8 评分及门控判断。

### 第 4 步：执行 P-13 至 P-15（渲染提交）
输出 HappyHorse 渲染提交清单、推荐画幅/时长/音频类型、RenderResult 占位模板。

### 第 5 步：执行 P-16 至 P-20（标注阶段）
建立 Annotation Table 独立标注表，执行 NoPost Audit 7 项附加检查。

### 第 6 步：执行 P-21 至 P-24（投放测试）
筛选可投放视频（HumanOverall ≥ 2 且 NoPostActual ≥ 2），生成 AdResult Table。

### 第 7 步：执行 P-25 至 P-29（Dashboard 与校准）
生成 Decision Dashboard 15 项、失败类型 Top 5、校准建议、Pilot Run Report。

---

## ⚠️ 防错规则

在 LLM（尤其是 DeepSeek）中使用本系统时，请注意以下最容易出错的地方：

1. **防止擅自扩展理论** — 当 LLM 开始提议升级版本时，立刻打断，强调只执行当前版本。
2. **防止把评分说成预测** — 强制 LLM 每次标注「评分为专家先验，不是投放效果预测」。
3. **防止跳过 Annotation 直接写 RenderResult** — 第一手标注必须进入 Annotation Table。
4. **防止把 Pilot 当 Level 1** — Pilot 只有 9 条视频，不满足 Level 1 的 30 条样本要求。
5. **防止混淆 v2.0.1 与 v2.1-MVP** — v2.0.1 是理论内核，v2.1-MVP 是执行手册。

---

## ❓ 常见问题 (FAQ)

**Q: 这个系统能保证视频的投放效果吗？**  
不能。本项目的评分权重基于专家先验，旨在提供创意与结构质量的参考，而非投放效果的预测。实际投放效果受平台算法、受众偏好等多重因素影响。

**Q: VEL 增强词是否会影响评分？**  
项目声明 VEL 增强词对评分的影响为中性至微幅正面，不会产生负面影响。

**Q: v2.0.1 和 v2.1-MVP 是什么关系？**  
v2.0.1 是理论内核，负责「怎么生成和评分」；v2.1-MVP 是执行手册，负责「怎么记录和执行」。两者配合使用，不可互相替代。

---

## 🤝 贡献指南

我们欢迎任何形式的贡献！你可以通过以下方式参与：

1. Fork 本仓库并创建你的特性分支 (`git checkout -b feature/amazing-feature`)
2. 提交你的更改 (`git commit -m 'Add some amazing feature'`)
3. 推送到分支 (`git push origin feature/amazing-feature`)
4. 开启一个 Pull Request

若有任何问题或建议，欢迎提交 [Issue](https://github.com/qq547820639/tiktok-ad-video-skill/issues)。

---

## 📄 许可证

本项目采用 [MIT License](https://opensource.org/licenses/MIT) 进行许可。

---

## ⚠️ 声明

- 本项目不是投放效果预测模型，所有权重为专家先验，待数据校准；
- VEL 增强词对评分的影响为中性至微幅正面；
- 输出内容仅供创作参考，实际投放前请根据平台规则进行合规性审查；
- Pilot 只有 9 条视频，只验证流程闭环，不满足 Level 1 的 30 条样本要求；
- 所有评分均为专家先验，不是投放效果预测；
- 不允许因为单条样本成功就宣称系统有效；
- 不允许因为单条样本失败就修改 Kernel。

---

> 由 [qq547820639](https://github.com/qq547820639) 维护 · 最后更新于 2026-05-08
