# 🎬 TikTok广告视频创意系统：HappyHorse CreativeOS + Seedance v3.5

> 一个完整的、可审计、可校准的AI视频广告创意编译器与TikTok投流Prompt生成系统，  
> 用于将产品卖点编译为可生成、可评分的优质广告视频素材。

---

## 📌 项目定位

**HappyHorse CreativeOS** 是一套面向TikTok广告创意的规则驱动型编译系统，融合了**创意编译器（Creative Compiler）**、**渲染评测器（Render Bench）**、**标注系统（Annotation Console）**、**投放追踪器（Ad Test Tracker）**、**校准引擎（Calibration Engine）** 以及**版本治理与决策看板**，实现从Prompt生成、结构质量评分、门控校验到投放资产输出的完整闭环。

**Seedance** 则是系统内的核心Prompt生成引擎（当前版本 **v3.5**），专为TikTok增长团队生成可直接投放的、符合Seedance 2.0规范的视频生成提示词（Prompt），同时包含视觉增强、创意诊断、迭代优化等完整工具链。

---

## 🧱 系统架构

```
┌─────────────────────────────────────────────────────────────────┐
│ HappyHorse CreativeOS v2.0.1 - v2.1-MVP                        │
├─────────────────────────────────────────────────────────────────┤
│ Layer 1: Kernel（精算内核）                                     │
│   规则 / 评分 / 门控 / 风险 / 奖励 / 惩罚 / 修复 / 回滚       │
├─────────────────────────────────────────────────────────────────┤
│ Layer 2: Runtime（执行器）                                      │
│   输入理解 / 模式路由 / 候选生成 / 评分 / 修复 / 收敛          │
├─────────────────────────────────────────────────────────────────┤
│ Layer 3: Delivery（交付界面）                                   │
│   Prompt / 标题 / 标签 / 评论 / Bio / 评分卡 / 风险声明         │
├─────────────────────────────────────────────────────────────────┤
│ Layer 4: Audit（审计模式）                                      │
│   14-Step Verification / 子特征 / KVS / EAD / CF/HU             │
├─────────────────────────────────────────────────────────────────┤
│ Layer 5: Evaluation（评测协议）                                  │
│   Render Test / NoPost Audit / Small Batch Ad Test              │
├─────────────────────────────────────────────────────────────────┤
│ Layer 6: Benchmark（评测工作台）                                 │
│   Test Set / Annotation Rubric / Error Taxonomy / Calibration    │
├─────────────────────────────────────────────────────────────────┤
│ Layer 7: Operations（运营系统）                                  │
│   Database / Dashboard / Version Governance / Team Roles        │
└─────────────────────────────────────────────────────────────────┘
```

---

## ✨ 核心特性

- **创意编译引擎**：基于8维特征（Q1-Q8）对每个广告创意进行结构化评分与诊断
- **视觉增强层（VEL v3.5）**：四类36个增强词库（物理真实 / 角色生命 / 材质光影 / 大气粒子），精准植入提升Prompt画面质量
- **双门控交付体系**：NoPostGate（零后期诚实边界）+ PostReady（商业投放就绪判定），支持用户选择“无需后期直接发布”或“标准后制兜底”模式
- **情绪弧分析（EAD）**：自动计算15秒内情绪切换密度，含LongFlatPenalty长平情绪检测与诊断修复建议
- **Seedance渲染置信度（PRC）**：按KVS（Key Visual Spec）逐项评估生成渲染可行性，辅助风险控制
- **Score-Guided迭代优化**：基于低分项自动触发Repair/Enhance循环，含完整IQD（迭代质量变化）记录
- **14步评分验算**：所有数值均可审计追溯
- **完整投放资产输出**：Prompt代码块、3类标题（反差/POV/情绪）、12-16标签、置顶评论、Bio CTA等一站式交付
- **数据库表结构设计（v2.1-MVP）**：包含9张核心表与18个视图，支持从产品信息到投放数据全链路追踪

---

## 📦 项目文档清单

| 文件 | 版本 | 内容概要 |
|------|------|----------|
| [**Seedance.md**](./Seedance.md) | v3.5 | Seedance Prompt生成系统完整规范，含VEL视觉增强层、8维评分体系、状态机、铁律（17条）、EAD情绪弧、PRC渲染置信度、NoPostGate/PostReady、迭代优化流程等 |
| [**HappyHorse CreativeOS v2.0.1**](./HappyHorse%20CreativeOS%20v2.0.1%20%E2%80%94%20%E7%B3%BB%E7%BB%9F%E8%A7%84%E8%8C%83%E5%AE%9A%E7%A8%BF) | v2.0.1 | 系统架构规范定稿，7层架构完整定义 |
| [**HappyHorse CreativeOS v2.1-MVP**](./HappyHorse%20CreativeOS%20v2.1-MVP%20%E2%80%94%20%E8%A1%A8%E6%A0%BC%E8%90%BD%E5%9C%B0%E7%89%88) | v2.1-MVP | 表格化落地执行版，9张数据库表 + 18个核心视图，提供工程化实现路径 |

---

## 📘 使用指南（DeepSeek操作手册）

### 核心使用理念

**不要把两份文档一股脑扔进去，而是按“系统宪法 + 执行手册 + 当前任务”三层投喂。**

- `v2.0.1` = 理论内核，负责 **如何生成、评分、审计、修复**
- `v2.1-MVP` = 表格落地执行手册，负责 **建表、填表、执行Pilot、Dashboard校准**
- DeepSeek 每次只执行**当前步骤**，禁止自由发挥

---

### 🚀 标准工作流（Pilot Run 七步法）

#### 第1步：建立工作上下文

首次打开对话时，先发系统指令，再粘贴两份文档。

**系统指令模板：**

```text
你是 HappyHorse CreativeOS 的系统执行代理。
你必须遵循《HappyHorse CreativeOS v2.0.1 系统规范定稿》作为理论内核，
并遵循《HappyHorse CreativeOS v2.1-MVP 表格落地版》作为执行层工作手册。

请严格区分：
1. v2.0.1 = 理论规范、评分内核、Prompt 生成与审计规则。
2. v2.1-MVP = 表格落地、18 个核心视图、Pilot 执行指南、Dashboard 与 CalibrationLog。
3. 所有评分均为专家先验，不是投放效果预测。
4. 不允许因为单条样本成功就宣称系统有效。
5. 不允许因为单条样本失败就修改 Kernel。
6. 不再扩展理论模块，除非我明确要求设计新版本。
7. 当前默认进入 v2.1-MVP Pilot Run 执行阶段。
8. 你的输出必须可复制、可执行、可填写进表格、可追溯。

接下来我会粘贴两份文档：
第一份是 v2.0.1 系统规范定稿；
第二份是 v2.1-MVP 表格落地版。
请先读取并建立工作上下文，不要立刻扩展理论。
```

**然后依次粘贴：**
- `【文档1】HappyHorse CreativeOS v2.0.1 系统规范定稿`
- `【文档2】HappyHorse CreativeOS v2.1-MVP 表格落地版`

**最后发送确认指令：**
```text
请读取以上两份文档，建立上下文。
读取后只回复：“已建立 HappyHorse CreativeOS 工作上下文。当前默认阶段：v2.1-MVP Pilot Run。”
不要总结，不要扩展理论。
```

---

#### 第2步：执行 P-01 ～ P-05（基础搭建）

```text
现在执行 v2.1-MVP Pilot Run 的 P-01 至 P-05。

请输出：
1. 建 9 张表的操作清单
2. 建 18 个核心视图的操作清单
3. 角色权限配置表
4. 3 个 Pilot 产品选择标准
5. Product Table 填写模板
6. 产品素材文件夹命名规则

不要生成 Prompt。
不要修改表结构。
不要扩展理论。
```

---

#### 第3步：执行 P-06 ～ P-12（生成候选 & 评分）

当你准备好3个产品信息后，发送：

```text
现在执行 P-06 至 P-12。

以下是 Product Table 的 3 条产品记录：
【粘贴产品信息】

请为每个产品生成 3 个候选：
A_StrongHook
B_EmotionReversal
C_ProductFunction

每个候选输出：
1. Prompt Table 填写内容
2. PreScore Table 填写内容
3. VEL Table 填写内容
4. Winner 选择理由，但 Pilot 阶段仍渲染全部 A/B/C

必须调用 v2.0.1 评分内核。
不要进入渲染标注阶段。
```

---

#### 第4步：执行 P-13 ～ P-15（提交渲染）

```text
现在执行 P-13 至 P-15。

以下是 9 条 Prompt：
【粘贴 Prompt Table / PromptText】

请输出：
1. HappyHorse 渲染提交清单
2. 每条 Prompt 的推荐画幅、时长、音频类型
3. RenderResult 占位记录模板
4. VideoID 命名规则
5. VideoLink 填写要求

注意：
RenderResult 此阶段只填写 VideoID / PromptID / VideoLink / RenderSuccess。
其他评分字段必须等 Annotation 独立标注后再聚合写入。
```

---

#### 第5步：执行 P-16 ～ P-20（独立标注阶段）

```text
现在执行 P-16 至 P-20：标注阶段。

以下是 9 条视频的 VideoID 和 VideoLink：
【粘贴视频链接】

请输出：
1. Annotation Table 独立标注表
2. 每条视频的评分维度说明
3. NoPost Audit 7 项附加检查模板
4. 分歧检查规则
5. RenderResult 聚合写入模板
6. FailureReason E1-E15 归类表

不要直接把 Annotation 跳过写入 RenderResult。
第一手标注必须进入 Annotation Table。
```

---

#### 第6步：执行 P-21 ～ P-24（投放测试）

```text
现在执行 P-21 至 P-24：投放测试阶段。

以下是 RenderResult 聚合结果：
【粘贴结果】

请筛选可投放视频：
HumanOverall ≥ 2 且 NoPostActual ≥ 2。

请输出：
1. 可投放视频列表
2. 每条视频推荐投放平台
3. AdResult Table 填写模板
4. 需要记录的投放指标
5. AudienceSignal 记录模板
```

---

#### 第7步：执行 P-25 ～ P-29（Dashboard & 校准）

```text
现在执行 P-25 至 P-29：Dashboard 与校准。

以下是 Product / Prompt / PreScore / RenderResult / AdResult / CalibrationLog 当前数据：
【粘贴数据】

请输出：
1. Decision Dashboard 15 项
2. 失败类型 Top 5
3. 需要校准模块 Top 5
4. 是否进入下一发布等级
5. CalibrationLog 写入内容
6. 下一轮测试建议
7. Pilot Run Report

注意：
Pilot 只有 9 条视频，不满足 Level 1 的 30 条样本要求。
判断 Level 1 时必须记录为样本不足，待扩展。
```

---

### 🧭 两份文档的调用边界

| 任务涉及 | 调用文档 | 典型指令 |
|----------|----------|----------|
| 生成 Prompt、计算 Q1-Q8、CreativeScore、PRC、EAD、NoPostGate、PostReady、VEL、ShowDontTell、低分诊断、Winner 选择、风险声明、审计 | `v2.0.1` | “请调用 v2.0.1 系统规范，基于以下产品信息生成 A/B/C 三个候选 Prompt…” |
| 建表、建视图、填表、Pilot 执行、RenderResult/Annotation/AdResult 记录、Dashboard 更新、CalibrationLog 写入 | `v2.1-MVP` | “请调用 v2.1-MVP 表格落地版，执行 P-04：选择 3 个产品并填写 Product Table…” |

---

### ⚠️ 常见易错点与纠正指令

1. **DeepSeek 擅自扩展理论** → 立刻打断：
   ```text
   停止扩展理论。当前只执行 v2.1-MVP Pilot Run。不得新增模块。
   ```

2. **将评分写成预测** → 强制声明：
   ```text
   评分为专家先验，不是投放效果预测。
   ```

3. **跳过 Annotation 直接写 RenderResult** → 明确流程：
   ```text
   RenderResult 只记录聚合后的最终标注结果，第一手标注必须进入 Annotation Table。
   ```

4. **误将 Pilot 视作 Level 1** → 提醒：
   ```text
   Pilot 只有 9 条视频，不满足 Level 1 的 30 条样本要求。Pilot 只验证流程闭环。
   ```

5. **混淆文档定位** → 重申：
   ```text
   v2.0.1 是理论内核，v2.1-MVP 是执行手册。
   ```

---

### 📌 长效使用建议

- **同一对话内**：首次投喂两份文档全文，后续只发当前任务 + 必要数据，不反复丢全文
- **新对话**：重新投喂系统指令 + 两份文档，或至少投喂相关章节
- **执行纪律**：始终明确当前步骤编号（P-xx）、输入、输出格式，并禁止扩展理论

> **核心口诀**  
> v2.0.1 负责“怎么生成和评分”；  
> v2.1-MVP 负责“怎么记录和执行”；  
> DeepSeek 每次只执行当前 P 步骤，不要自由发挥。

---

## 🛠️ 技术栈

- **核心协议**：Seedance 2.0 视频生成提示词规范
- **编程范式**：规则驱动 + 专家先验评分 + 数据后验校准
- **数据库设计**：关系型表格结构（9表 + 18视图）
- **渲染引擎**：Seedance 2.0（文生视频、图生视频、视频编辑、音视频联合生成）

---

## 📐 声明与限制

1. **所有评分均为专家先验，非投放效果预测**。只有接入真实生成数据和投放数据并完成校准后，才允许讨论预测关系。
2. 支持的视频类型：Seedance 2.0 AI视频（默认），时长15秒，9:16竖屏。
3. 不支持：精准品牌名/Logo的精确生成、精确色彩控制、复杂时间效果（如时间倒流）、分屏效果。

---

## 📝 参与贡献

欢迎通过Issue或PR参与项目改进。贡献方向包括但不限于：

- 视觉增强词库扩展与优化
- 品类/市场相关评分参数调优
- 数据库表结构和视图的工程化实现
- 投放数据回传后的校准算法实现
- 仪表盘（Dashboard）的可视化设计

---

## 📄 许可

本项目文档仅供学习与参考。所有创意评测方法、评分体系、视觉增强层（VEL）设计等知识产权归原仓库作者所有。
