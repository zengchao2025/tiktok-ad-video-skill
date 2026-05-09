# HappyHorse CreativeOS v2.1-MVP — 表格落地版

---

## 系统定位

```text
HappyHorse CreativeOS v2.1-MVP
= v2.0.1 系统规范定稿的表格落地执行版本
= 9 张数据库表 + 18 个核心视图 + Pilot 执行指南 + Decision Dashboard

理论基础：HappyHorse CreativeOS v2.0.1 系统规范定稿
执行目标：用 3 产品 × 3 候选 = 9 条视频验证从 Prompt 生成到渲染标注到投放校准的完整闭环
```

**声明：** 所有评分仍为专家先验，不是投放效果预测。只有接入真实生成数据和投放数据并完成校准后，才允许讨论预测关系。

---

## 版本依据链

```text
v2.0 系统性检阅
  → v2.0.1 修订依据
    → 12 项主补丁
      → 4 项 Minor Clarification
        → 6 项 Final Micro-Fix（SS残留 / B5合并 / SCScore统一 / Audit口径 / PRC优先级 / 字段职责）
          → 9 项 Table Micro-Fix（关系图 / Category / 数值口径 / PostReady / 复合键 / PromptID / CandidateType / 追溯 / 阶段必填）
            → 6 项 View Micro-Fix（Pilot阶段判断 / Annotation入口 / NoPost匹配 / Q8映射 / Kanban替代 / B5同步）
              → 10 项 Pilot Micro-Fix（品类 / Winner / 占位记录 / 视频入口 / 口径统一 / 投放标准 / 表数量 / Level1 / 单条限制 / NoAction）
                → 5 项 Pilot Execution Micro-Fix（标题口径 / P-14写入 / 音频口径 / NoAction必填 / 角色验证）
                  → 7 项 Final Tabletop Micro-Fix（VideoLink / NoPostActual映射 / Level3口径 / Kanban兜底 / 分歧兜底 / CalibrationLog待定 / Rollup兜底）
```

---

# 第一部分：9 张表结构

---

## 一、表间关系总览

```
Product Table（产品主表）
  │ 1:N
  ▼
Prompt Table（Prompt 主表）
  ├── 1:1 → PreScore Table（预评分）
  ├── 1:N → RenderResult Table（渲染结果）
  │           ├── 1:N → AdResult Table（投放数据）
  │           ├── 1:N → Annotation Table（独立标注）
  │           └── 1:1 → Series Table（系列连贯性，仅系列内容）
  └── 1:N → VEL Table（VEL 植入记录）

CalibrationLog Table（校准日志）
  独立记录版本校准日志，不直接绑定单条 Prompt
  TriggeredByData 字段中记录触发样本的 VideoID / PromptID / 指标摘要
```

---

## 二、Product Table

- **表用途：** 存储产品基础信息，作为所有 Prompt 和视频记录的上游主表。
- **主键：** ProductID
- **是否核心表：** 是

| 字段名 | 字段类型 | 是否必填 | 枚举/取值范围 | 说明 |
|:--|:--|:--|:--|:--|
| ProductID | 文本（单行文本） | 是 | 如 `PROD-001` | 产品唯一标识 |
| ProductName | 文本（单行文本） | 是 | 自由文本 | 产品名称 |
| Category | 单选 | 是 | 美妆 / 穿搭 / 食品 / 数码 / 工具 / 软件 / 设备 / 家居 / 生活方式 / 其他 | 品类（仅真实品类，不含价格属性） |
| PriceBand | 文本（单行文本） | 是 | 低客单价 / 中客单价 / 中高客单价 / 高客单价 / 自定义价格段 | 价格带 |
| Market | 文本（单行文本） | 是 | 如 中国大陆 / 东南亚 / 北美 / 欧洲 | 目标市场 |
| TargetAudience | 文本（长文本） | 是 | 自由文本 | 目标人群描述 |
| CoreSellingPoint | 文本（长文本） | 是 | 自由文本 | 核心卖点 |
| UseCase | 文本（长文本） | 是 | 自由文本 | 使用场景 |
| CreatedDate | 日期 | 是 | 日期格式 | 创建日期 |

**Rollup 字段：**

| 字段名 | 类型 | 来源 | 计算逻辑 | 落地兜底 |
|:--|:--|:--|:--|:--|
| PromptCount | Rollup | Prompt（通过 ProductID） | COUNT | — |
| VideoCount | Rollup | RenderResult（通过 PromptID） | COUNT | 若平台不支持 Product → Prompt → RenderResult 跨层 Rollup，则先在 Prompt Table 中汇总 VideoCount，再由 Product Table Rollup Prompt.VideoCount |
| Avg_CreativeScore | Rollup | PreScore（通过 PromptID） | AVG(CreativeScore_Pre) | — |

**素材管理：** 产品图存储在外部素材文件夹中，命名规则 `/ProductAssets/PROD-001/product_main.jpg`。

---

## 三、Prompt Table

- **表用途：** 存储每条 Prompt 的完整内容及配套投放资产。
- **主键：** PromptID
- **关联字段：** ProductID → Product Table
- **是否核心表：** 是

| 字段名 | 字段类型 | 是否必填 | 枚举/取值范围 | 说明 |
|:--|:--|:--|:--|:--|
| PromptID | 文本（单行文本） | 是 | 如 `PROMPT-PROD001-A-v1` | Prompt 唯一标识 |
| ProductID | 关联（Relation） | 是 | 关联 Product Table | 关联产品 |
| PromptVersion | 文本（单行文本） | 是 | 如 `v1` / `v2` / `v1-r1` | 版本号 |
| CandidateType | 单选 | 是 | A_StrongHook / B_EmotionReversal / C_ProductFunction | 候选类型 |
| HappyHorseMode | 单选 | 是 | T2V / I2V / R2V / V2V | 生成模式 |
| PromptText | 文本（长文本） | 是 | 中文 ≤2500 汉字，英文 ≤5000 字符 | 完整 Prompt |
| TitleA | 文本（单行文本） | 否 | 自由文本 | 反差型标题 |
| TitleB | 文本（单行文本） | 否 | 自由文本 | POV 型标题 |
| TitleC | 文本（单行文本） | 否 | 自由文本 | 情绪型标题 |
| TitleD | 文本（单行文本） | 否 | 自由文本 | 功能型标题 |
| Tags | 文本（单行文本） | 否 | 12-16 个，逗号分隔 | 标签 |
| PinnedComment | 文本（长文本） | 否 | 自由文本 | 置顶评论 |
| BioCTA | 文本（单行文本） | 否 | 自由文本 | Bio CTA |
| ProductCardCopy | 文本（单行文本） | 否 | 自由文本 | 商品卡文案 |
| CreatedDate | 日期 | 是 | 日期格式 | 创建日期 |

---

## 四、PreScore Table

- **表用途：** 存储每条 Prompt 的专家先验预评分，包括完整评分链。
- **主键：** PromptID（一对一关联 Prompt Table）
- **关联字段：** PromptID → Prompt Table
- **是否核心表：** 是

| 字段名 | 字段类型 | 是否必填 | 枚举/取值范围 | 说明 |
|:--|:--|:--|:--|:--|
| PromptID | 关联（Relation） | 是 | 关联 Prompt Table | 关联 Prompt |
| CreativeScore_Pre | 数值（数字） | 是 | 0-100 | 最终创意分 |
| Q1_Pre | 数值（数字） | 是 | 0-5 | HookPower |
| Q2_Pre | 数值（数字） | 是 | 0-5 | ProductPower |
| Q3_Pre | 数值（数字） | 是 | 0-5 | SensoryRichness |
| Q4_Pre | 数值（数字） | 是 | 0-5 | Spreadability |
| Q5_Pre | 数值（数字） | 是 | 0-5 | ExecutionPower |
| Q6_Pre | 数值（数字） | 是 | 0-5 | GrowthDelivery |
| Q7_Pre | 数值（数字） | 是 | 0-5 | HappyHorseReliability |
| Q8_Pre | 数值（数字） | 是 | 0-5 | EmotionalImpact |
| PRC_Pre | 单选 | 是 | High / Medium / Low | 渲染置信度 |
| EAD_Pre | 单选 | 是 | High / Medium / Low | 情绪弧密度 |
| NoPostGate_Pre | 单选 | 是 | 通过 / 谨慎通过 / 不通过 | NoPost 判断 |
| PostReady_Pre | 单选 | 是 | 通过 / 谨慎通过 / 不通过 | PostReadyScore 换算后的等级 |
| CF_Pre | 单选 | 是 | High / Medium / Low | 评分置信度 |
| HU_Pre | 单选 | 是 | Low / Medium / High | 启发式不确定性 |
| U_domain | 数值（保留2位小数） | 是 | 0.00-1.00 | 四域效用 |
| G_gate | 数值（保留2位小数） | 是 | 0.00-1.00 | 门控乘数 |
| R_risk | 数值（保留2位小数） | 是 | 0.78-1.00 | 风险折扣 |
| B_bonus | 数值（保留3位小数） | 是 | 1.000-1.060 | 饱和奖励 |
| P_penalty | 数值（整数） | 是 | ≥0 | 线性惩罚（非负值） |

**说明：** PostReady_Pre 为 PostReadyScore（满分 6 分）换算后的等级：6=通过，4-5=谨慎通过，≤3=不通过。MVP 第一版不单独存储 P1-P6 和 PostReadyScore，审计阶段如需展开可在后续视图或公式层补充。

**Rollup 字段：**

| 字段名 | 类型 | 来源 | 计算逻辑 |
|:--|:--|:--|:--|
| VideoCount | Rollup | RenderResult（通过 PromptID） | COUNT |
| Avg_HumanOverall | Rollup | RenderResult（通过 PromptID） | AVG(HumanOverall) |
| RenderSuccess_Rate | Formula | VideoCount + RenderResult | COUNT(RenderSuccess=2)/VideoCount×100% |

---

## 五、RenderResult Table

- **表用途：** 存储每条生成视频的聚合后最终标注结果。只记录最终结果，不作为第一手独立标注入口。
- **主键：** VideoID
- **关联字段：** PromptID → Prompt Table
- **是否核心表：** 是

| 字段名 | 字段类型 | 是否必填 | 枚举/取值范围 | 说明 |
|:--|:--|:--|:--|:--|
| VideoID | 文本（单行文本） | 是 | 如 `VID-001-A-v1-01` | 视频唯一标识 |
| PromptID | 关联（Relation） | 是 | 关联 Prompt Table | 关联 Prompt |
| VideoLink | 文本（URL/单行文本） | 是 | 可点击视频链接或附件 | **v2.1-MVP 执行层必要字段**，用于承接实际视频文件，不改变 v2.0.1 理论评分结构 |
| RenderSuccess | 数值（整数） | 创建时必填 | 2 / 1 / 0 | 2=完整成功，1=部分成功，0=失败 |
| VisualQuality | 数值（整数） | 标注后必填 | 2 / 1 / 0 | 2=可投放级，1=可用但一般，0=不可用 |
| ProductVisibility | 数值（整数） | 标注后必填 | 2 / 1 / 0 | 2=清晰可见，1=部分可见，0=不清楚 |
| MotionAccuracy | 数值（整数） | 标注后必填 | 2 / 1 / 0 | 2=符合 Prompt，1=部分符合，0=明显不符合 |
| FaceBodyStabilityScore | 数值（整数） | 标注后必填 | 2 / 1 / 0 | 2=稳定，1=轻微异常，0=明显异常 |
| FaceBodyApplicable | 单选 | 标注后必填 | Yes / No | 是否涉及人物 |
| AudioMatchScore | 数值（整数） | 标注后必填 | 2 / 1 / 0 | 2=自然匹配，1=基本匹配，0=不匹配 |
| AudioApplicable | 单选 | 标注后必填 | Yes / No | 是否涉及音频 |
| TextQualityScore | 数值（整数） | 标注后必填 | 2 / 1 / 0 | 2=无错误，1=轻微错误，0=严重错误 |
| PRC_Actual | 单选 | 标注后必填 | High / Medium / Low | 实际渲染置信度 |
| NoPostActual | 数值（整数） | 标注后必填 | 3 / 2 / 1 / 0 | 映射见下方 |
| ReworkNeeded | 单选 | 标注后必填 | None / Minor / Major | 是否需要返工 |
| FailureReason_Main | 单选 | 否 | E1-E15 | 主失败原因 |
| FailureReason_Secondary | 单选 | 否 | E1-E15 | 次失败原因 |
| HumanOverall | 数值（整数） | 标注后必填 | 3 / 2 / 1 / 0 | 3=可直接投放，2=小修可投放，1=需要重做，0=不可用 |
| PrimaryAnnotatorID | 文本（单行文本） | 否 | 自由文本 | 可选，单标注者记录该标注者；多标注者记录复审负责人 |
| AnnotationDate | 日期 | 标注后必填 | 日期格式 | 标注日期 |

**NoPostActual 统一映射：**

| 数值 | 文本标签 | 含义 |
|:--|:--|:--|
| 3 | DirectReady | 无需后期可直接发布 |
| 2 | LightEdit | 主体可用，建议轻微剪辑 |
| 1 | NeedsPost | 必须后期处理才可发布 |
| 0 | Reject | 不可发布 |

所有 NoPost 视图、Dashboard 和公式均按该映射执行。

**阶段性必填说明：** 渲染后创建占位记录，仅填写 VideoID / PromptID / VideoLink / RenderSuccess。正式评分字段由 Annotation 独立标注后，再由复审负责人聚合写入。

**Formula 字段：**

| 字段名 | 计算逻辑 | 用途 |
|:--|:--|:--|
| NoPost_Mismatch | 分类匹配（见视图设计第六节） | 标记 NoPostGate_Pre 与 NoPostActual 偏差 |
| PRC_Mismatch | 等级匹配（见视图设计第七节） | 标记 PRC_Pre 与 PRC_Actual 偏差 |
| IsPublishable | IF(NoPostActual ≥ 2, "是", "否") | 是否可发布 |

**Rollup 字段：**

| 字段名 | 来源 | 用途 |
|:--|:--|:--|
| CreativeScore_Pre | PreScore（通过 PromptID） | Pilot 看板 |
| PRC_Pre | PreScore（通过 PromptID） | PRC 偏差追踪 |
| NoPostGate_Pre | PreScore（通过 PromptID） | NoPost 风险追踪 |
| Q1_Pre | PreScore（通过 PromptID） | Q1/Q8 Signal |
| Q8_Pre | PreScore（通过 PromptID） | Q1/Q8 Signal |
| EAD_Pre | PreScore（通过 PromptID） | EAD 掉点追踪 |
| AdTestCount | AdResult（通过 VideoID） | 投放测试次数 |

---

## 六、AdResult Table

- **表用途：** 存储每条可发布视频的小样本投放测试数据。
- **主键：** VideoID + Platform + TestDate（复合键，公式主显示名）
- **关联字段：** VideoID → RenderResult Table
- **是否核心表：** 是

| 字段名 | 字段类型 | 是否必填 | 枚举/取值范围 | 说明 |
|:--|:--|:--|:--|:--|
| VideoID | 关联（Relation） | 是 | 关联 RenderResult | 关联视频 |
| Platform | 单选 | 是 | TikTok / Reels / Shorts / 小红书 / 其他 | 投放平台 |
| Spend | 数值（保留2位小数） | 是 | ≥0 | 测试预算 |
| Impressions | 数值（整数） | 是 | ≥0 | 曝光量 |
| ThreeSecondViewRate | 数值（保留1位小数） | 是 | 0-100 | 3 秒停留率 |
| CompletionRate | 数值（保留1位小数） | 是 | 0-100 | 完播率 |
| RewatchRate | 数值（保留1位小数） | 否 | 0-100 | 复播率 |
| LikeRate | 数值（保留2位小数） | 否 | 0-100 | 点赞率 |
| CommentRate | 数值（保留2位小数） | 否 | 0-100 | 评论率 |
| ShareRate | 数值（保留2位小数） | 否 | 0-100 | 分享率 |
| CTR | 数值（保留2位小数） | 否 | 0-100 | 点击率 |
| CVR | 数值（保留2位小数） | 否 | 0-100 | 转化率 |
| CPA | 数值（保留2位小数） | 否 | ≥0 | 单次转化成本 |
| ROAS | 数值（保留2位小数） | 否 | ≥0 | 广告支出回报 |
| ROI | 数值（保留2位小数） | 否 | 可为负 | 投资回报率 |
| RetentionCurveLink | 文本（URL） | 否 | URL 或文件路径 | 留存曲线 |
| MajorDropoffSecond | 数值（整数） | 否 | 1-15 | 主要掉点秒数 |
| MidpointRetentionRate | 数值（保留1位小数） | 否 | 0-100 | 中点留存率 |
| DropoffNote | 文本（长文本） | 否 | 自由文本 | 掉点模式描述 |
| AudienceSignal | 文本（长文本） | 否 | 自由文本 | 评论情绪/收藏意图/购买意图/质疑点 |
| TestDate | 日期 | 是 | 日期格式 | 测试日期 |

**落地注意：** 3 层 Rollup（AdResult → RenderResult → Prompt → PreScore）在 Airtable 中需通过 Formula 辅助字段或脚本实现。MVP 第一版建议在 AdResult 中手动复制 Q1_Pre / Q8_Pre / EAD_Pre。

---

## 七、CalibrationLog Table

- **表用途：** 记录每次校准动作的完整信息，确保所有 Kernel 级修改有据可查。
- **主键：** CalibrationID
- **是否核心表：** 是

| 字段名 | 字段类型 | 是否必填 | 枚举/取值范围 | 说明 |
|:--|:--|:--|:--|:--|
| CalibrationID | 文本（单行文本） | 是 | 如 `CAL-v2.0.1-001` | 校准唯一标识 |
| VersionBefore | 文本（单行文本） | 是 | 如 `v2.0.1` | 修改前版本 |
| VersionAfter | 文本（单行文本） | 是 | 如 `v2.0.1-r1`；待评估时填写"待定" | 修改后版本 |
| TriggeredByData | 文本（长文本） | 是 | 自由文本，必须记录触发样本的 VideoID / PromptID / 指标摘要 | 触发数据 |
| ProblemDetected | 文本（长文本） | 是 | 自由文本 | 发现的问题 |
| ModuleChanged | 单选 | 是 | Kernel / Runtime / Delivery / Audit / Evaluation / Benchmark / Operations | 修改模块 |
| RuleBefore | 文本（长文本） | 是 | 自由文本；待评估时填写"待定" | 修改前规则 |
| RuleAfter | 文本（长文本） | 是 | 自由文本；待评估时填写"待定" | 修改后规则 |
| ExpectedImprovement | 文本（长文本） | 是 | 自由文本 | 预期改善 |
| ActionLevel | 单选 | 是 | 1 / 2 / 3 | 1=文案级，2=Prompt级，3=Kernel级 |
| RollbackCondition | 文本（长文本） | 是 | 自由文本 | 回滚条件 |
| Owner | 文本（单行文本） | 是 | 自由文本 | 负责人 |
| Date | 日期 | 是 | 日期格式 | 修改日期 |

**待评估记录规则：** 因 VersionAfter / RuleAfter 为必填字段，不使用空值判断。待评估记录中 VersionAfter / RuleAfter 填写"待定"；已执行记录中 VersionAfter / RuleAfter 不为"待定"。

**NoActionNeeded 记录规则：** 若本轮未触发校准需求，仍需创建记录以满足必填约束：

| 字段 | NoActionNeeded 时填写值 |
|:--|:--|
| ProblemDetected | "NoActionNeeded：本轮未触发校准需求" |
| VersionAfter | 与 VersionBefore 相同 |
| ModuleChanged | Operations |
| RuleBefore | "无变更" |
| RuleAfter | "无变更" |
| ExpectedImprovement | "无需改善" |
| ActionLevel | 1 |
| RollbackCondition | "不适用" |

---

## 八、VEL Table（扩展表）

- **表用途：** 记录每条 Prompt 中 VEL 视觉增强层的植入详情。
- **主键：** 公式字段 `PromptID + "-" + VEL_Type + "-" + VEL_Position`（如同一位置出现重复 VEL，追加序号）
- **关联字段：** PromptID → Prompt Table
- **是否核心表：** 否

| 字段名 | 字段类型 | 是否必填 | 枚举/取值范围 | 说明 |
|:--|:--|:--|:--|:--|
| PromptID | 关联（Relation） | 是 | 关联 Prompt Table | 关联 Prompt |
| VEL_Type | 单选 | 是 | A / B / C / D | A=物理真实，B=角色生命，C=材质光影，D=大气粒子 |
| VEL_Content | 文本（单行文本） | 是 | 自由文本 | 具体增强词 |
| VEL_Position | 文本（单行文本） | 是 | 如 `第3句` | 植入位置 |
| VEL_RenderResult | 单选 | 否 | 有效 / 无效 / 堆叠 / 冲突 | 渲染后填写 |
| CreatedDate | 日期 | 是 | 日期格式 | 创建日期 |

---

## 九、Annotation Table（扩展表）

- **表用途：** 记录每位标注者的独立评分，用于支持多标注者独立打分和分歧计算。
- **主键：** AnnotationID
- **关联字段：** VideoID → RenderResult Table
- **是否核心表：** 否

| 字段名 | 字段类型 | 是否必填 | 枚举/取值范围 | 说明 |
|:--|:--|:--|:--|:--|
| AnnotationID | 文本（单行文本） | 是 | 如 `ANN-001-01` | 标注唯一标识 |
| VideoID | 关联（Relation） | 是 | 关联 RenderResult | 关联视频 |
| AnnotatorID | 文本（单行文本） | 是 | 自由文本 | 标注者标识 |
| RenderSuccess | 数值（整数） | 是 | 2 / 1 / 0 | |
| VisualQuality | 数值（整数） | 是 | 2 / 1 / 0 | |
| ProductVisibility | 数值（整数） | 是 | 2 / 1 / 0 | |
| MotionAccuracy | 数值（整数） | 是 | 2 / 1 / 0 | |
| FaceBodyStabilityScore | 数值（整数） | 是 | 2 / 1 / 0 | |
| FaceBodyApplicable | 单选 | 是 | Yes / No | |
| AudioMatchScore | 数值（整数） | 是 | 2 / 1 / 0 | |
| AudioApplicable | 单选 | 是 | Yes / No | |
| TextQualityScore | 数值（整数） | 是 | 2 / 1 / 0 | |
| NoPostActual | 数值（整数） | 是 | 3 / 2 / 1 / 0 | |
| HumanOverall | 数值（整数） | 是 | 3 / 2 / 1 / 0 | |
| Notes | 文本（长文本） | 否 | 自由文本（含 NoPost Audit 7 项附加检查） | 标注备注 |
| AnnotationDate | 日期 | 是 | 日期格式 | |

---

## 十、Series Table（扩展表）

- **表用途：** 仅在系列/连载/EP/campaign 时使用。非系列内容不使用此表。
- **主键：** SeriesID + EpisodeNumber
- **关联字段：** VideoID → RenderResult Table
- **是否核心表：** 否

| 字段名 | 字段类型 | 是否必填 | 枚举/取值范围 | 说明 |
|:--|:--|:--|:--|:--|
| SeriesID | 文本（单行文本） | 是 | 如 `SER-001` | 系列唯一标识 |
| SeriesName | 文本（单行文本） | 是 | 自由文本 | 系列名称 |
| EpisodeNumber | 数值（整数） | 是 | ≥1 | 集数 |
| VideoID | 关联（Relation） | 是 | 关联 RenderResult | 关联视频 |
| CharacterConsistency | 数值（数字） | 是 | 0-5 | 角色一致性 |
| WorldConsistency | 数值（数字） | 是 | 0-5 | 世界观一致性 |
| VisualStyleConsistency | 数值（数字） | 是 | 0-5 | 视觉风格一致性 |
| CTAConsistency | 数值（数字） | 是 | 0-5 | CTA 节奏一致性 |
| EmotionContinuity | 数值（数字） | 是 | 0-5 | 情绪衔接 |
| SCScore | Formula | 是 | 0-5 | (五项之和)/5，自动计算 |
| SeriesFollowRate | 数值（保留1位小数） | 否 | 0-100 | 系列追看率 |
| Notes | 文本（长文本） | 否 | 自由文本 | |
| CreatedDate | 日期 | 是 | 日期格式 | |

---

# 第二部分：18 个核心视图设计

---

## 一、9 个默认视图

每张表打开时的基础视图，展示全部记录、全部字段。

| 编号 | 视图名称 | 基于表 | 视图类型 | 排序 | 分组 |
|:--|:--|:--|:--|:--|:--|
| 1 | 全部产品 | Product | Grid | CreatedDate 降序 | Category |
| 2 | 全部 Prompt | Prompt | Grid | CreatedDate 降序 | ProductID |
| 3 | 全部预评分 | PreScore | Grid | CreativeScore_Pre 降序 | PRC_Pre |
| 4 | 全部渲染结果 | RenderResult | Grid | AnnotationDate 降序 | RenderSuccess |
| 5 | 全部投放数据 | AdResult | Grid | TestDate 降序 | Platform |
| 6 | 全部校准记录 | CalibrationLog | Grid | Date 降序 | ActionLevel |
| 7 | 全部 VEL 记录 | VEL | Grid | CreatedDate 降序 | VEL_Type |
| 8 | 全部独立标注 | Annotation | Grid | AnnotationDate 降序 | VideoID |
| 9 | 全部系列记录 | Series | Grid | CreatedDate 降序 | SeriesID |

---

## 二、Pilot 执行看板（视图 #10）

- **基于表：** Prompt Table
- **视图类型：** Kanban
- **服务对象：** Creative Operator
- **阶段判断：** 由关联记录状态决定

| 泳道 | 筛选条件 | 含义 |
|:--|:--|:--|
| 待预评分 | PromptID 在 PreScore 中无记录 | Prompt 已创建，等待评分 |
| 待渲染 | PreScore 有记录，RenderResult 无记录 | 已评分，等待渲染 |
| 待标注 | RenderResult 有记录，HumanOverall 为空 | 已渲染，等待标注 |
| 标注完成 | HumanOverall 已填写，AdResult 无记录 | 可进入投放 |
| 已投放 | AdResult 有对应 VideoID | 已进入投放测试 |

**显示字段：** PromptID / ProductID / CandidateType / HappyHorseMode / CreativeScore_Pre / PRC_Pre / NoPostGate_Pre / RenderSuccess / HumanOverall

**排序：** CreativeScore_Pre 降序

**落地兜底：** 若平台不支持跨表公式作为 Kanban 分组，则用 5 个筛选视图替代：待预评分 / 待渲染 / 待标注 / 标注完成 / 已投放。

---

## 三、独立标注视图（视图 #11）

- **基于表：** Annotation Table
- **服务对象：** Render Reviewer
- **筛选：** 当前 AnnotatorID 的记录，HumanOverall 为空
- **排序：** AnnotationDate 升序
- **用途：** 第一手独立标注入口。RenderResult 不作为第一手标注入口。

---

## 四、标注分歧检查视图（视图 #12）

- **基于表：** Annotation Table
- **服务对象：** Render Reviewer
- **筛选：** 同一 VideoID 下不同 AnnotatorID 的 HumanOverall 分歧 > 1
- **排序：** 分歧值降序
- **显示字段：** VideoID / AnnotatorID / HumanOverall / 分歧值
- **用途：** 分歧 > 1 时必须进入复审流程。
- **落地兜底：** 若平台不支持跨记录 MAX-MIN 自动计算，则在分歧检查视图中人工判断同一 VideoID 下不同 AnnotatorID 的 HumanOverall 分歧。

---

## 五、最终复审视图（视图 #13）

- **基于表：** RenderResult Table
- **服务对象：** PrimaryAnnotatorID
- **筛选：** AnnotationDate 为空
- **用途：** 将 Annotation 聚合后的最终结果写入 RenderResult。

---

## 六、NoPost 风险追踪视图（视图 #14）

- **基于表：** RenderResult Table
- **服务对象：** Render Reviewer + Calibration Owner
- **筛选：** NoPostActual ≤ 1
- **排序：** NoPostActual 升序

**NoPost_Mismatch 分类匹配规则：**

| NoPostGate_Pre | 预期 NoPostActual | 匹配结果 |
|:--|:--|:--|
| 通过 | DirectReady（3） | 一致 |
| 通过 | LightEdit（2） | 轻微偏差 |
| 通过 | NeedsPost（1）或 Reject（0） | 严重偏差（高估） |
| 谨慎通过 | LightEdit（2） | 一致 |
| 谨慎通过 | DirectReady（3） | 轻微偏差（低估） |
| 谨慎通过 | NeedsPost（1） | 轻微偏差 |
| 谨慎通过 | Reject（0） | 严重偏差 |
| 不通过 | NeedsPost（1）或 Reject（0） | 一致 |
| 不通过 | DirectReady（3）或 LightEdit（2） | 严重偏差（低估） |

Dashboard 一致率只统计"一致"记录，轻微偏差单独统计为参考项。

---

## 七、PRC 偏差追踪视图（视图 #15）

- **基于表：** RenderResult Table
- **服务对象：** Calibration Owner
- **筛选：** PRC_Actual 比 PRC_Pre 低至少一个等级

**PRC_Mismatch 公式：**

| PRC_Pre | PRC_Actual | 结果 |
|:--|:--|:--|
| High | Low | 严重偏差 |
| High | Medium | 轻度偏差 |
| Medium | Low | 轻度偏差 |
| 其他 | — | 一致 |

**PRC 判定保守优先级：** 若描述性风险条件与 KVS 低置信项数量冲突，采用更保守等级。即任一中/低风险条件触发时，PRC 不得高于对应风险等级。

---

## 八、Q1/Q8 投放信号追踪视图（视图 #16）

- **基于表：** AdResult Table
- **服务对象：** Calibration Owner + Ad Tester

**筛选条件（任一触发）：**

| 筛选条件 | 校准映射 |
|:--|:--|
| Q1_Pre ≥ 4 且 ThreeSecondViewRate < 35% | 校准 Q1#1-Q1#3（声音事件、视觉冲突、动作动词） |
| Q8_Pre ≥ 4 且 ThreeSecondViewRate < 35% | 校准 Q8#1（Hook 情绪冲击，检查前 0.5 秒强触发） |
| Q8_Pre ≥ 4 且 RewatchRate < 15% | 校准 Q8#4（结尾反预期） |
| Q8_Pre ≥ 4 且 CompletionRate 低于品类中位数 | 校准 Q8#2/Q8#5（情绪段和前后情绪变化） |

MVP 第一版品类中位数使用固定阈值（如 CompletionRate < 40%），积累数据后调整。

**样本量兜底：** 高分组或低分组样本数 < 3 时标记 "Insufficient Sample"，不判断区分度。

---

## 九、EAD 曲线掉点追踪视图（视图 #17）

- **基于表：** AdResult Table
- **服务对象：** Calibration Owner
- **筛选：** EAD_Pre = "High" 且 MajorDropoffSecond 在 4-10 秒之间
- **显示字段：** VideoID / EAD_Pre / CompletionRate / MajorDropoffSecond / MidpointRetentionRate / DropoffNote

---

## 十、校准待办视图（视图 #18）

- **基于表：** CalibrationLog Table
- **视图类型：** Grid（筛选视图）
- **服务对象：** Calibration Owner

| 分组 | 筛选条件 | 含义 |
|:--|:--|:--|
| 待评估 | VersionAfter = "待定"，RuleAfter = "待定" | 已识别问题，待评估 |
| 已执行 | VersionAfter 不为"待定"，RuleAfter 不为"待定"，且不为 NoActionNeeded | 校准已执行 |
| 需观察 | ExpectedImprovement 已填写，后续验证数据不足 | 等待验证 |
| 已回滚 | TriggeredByData 或 ProblemDetected 中记录回滚 | 已回滚 |

**排序：** ActionLevel 降序 → Date 升序

---

## 十一、Decision Dashboard 15 项输出

| 编号 | 输出项 | 数据来源 | 计算方式 | 基准 |
|:--|:--|:--|:--|:--|
| 1 | 测试产品数 | Product | COUNT | — |
| 2 | 生成视频数 | RenderResult | COUNT | — |
| 3 | RenderSuccess 比例 | RenderResult | COUNT(=2)/总×100% | ≥80% |
| 4 | DirectReady 比例 | RenderResult | COUNT(NoPostActual=3)/总×100% | — |
| 5 | LightEdit 比例 | RenderResult | COUNT(NoPostActual=2)/总×100% | #4+#5 ≥70% |
| 6 | Reject 比例 | RenderResult | COUNT(NoPostActual=0)/总×100% | ≤15% |
| 7 | PRC 一致率 | PreScore+RenderResult | COUNT(PRC_Pre=PRC_Actual)/总×100% | ≥70% |
| 8 | NoPost 一致率 | PreScore+RenderResult | 分类匹配"一致"数/总×100% | ≥70% |
| 9 | Q1 高低分组 3秒率差异 | PreScore+AdResult | 高分组均值-低分组均值 | ≥5pp 或 ≥15% |
| 10 | Q8 高低分组 完播/复播差异 | PreScore+AdResult | 高分组均值-低分组均值 | ≥5pp 或 ≥15% |
| 11 | 失败类型 Top 5 | RenderResult | FailureReason_Main 分组 | — |
| 12 | 校准模块 Top 5 | CalibrationLog | ModuleChanged 分组 | — |
| 13 | 本轮校准动作 | CalibrationLog | 列表 | — |
| 14 | 是否进入下一发布等级 | 手动判断 | O3 Level 0-4 条件 | — |
| 15 | 下一轮测试建议 | Calibration Owner | 自由文本 | — |

---

## 十二、角色权限

| 角色 | 读写表 | 只读表 | 关键视图 |
|:--|:--|:--|:--|
| Creative Operator | Product / Prompt / VEL | 其余 | Pilot 执行看板 |
| Render Reviewer | RenderResult / Annotation / Series | 其余 | 独立标注 / 分歧检查 / 最终复审 / NoPost 风险 |
| Ad Tester | AdResult | 其余 | Q1/Q8 Signal |
| Calibration Owner | PreScore / CalibrationLog | 其余 | PRC 偏差 / EAD 掉点 / 校准待办 / Dashboard |
| 个人项目 | 全部读写 | — | 全部视图 |

---

# 第三部分：Pilot 执行指南

---

> **说明：** 本文档为 Pilot 执行指南，描述执行方案和操作步骤。Pilot 实际执行完成后，应输出独立的 Pilot Run Report，记录 Decision Dashboard 15 项输出、校准判断和下轮建议。

---

## 一、Pilot 总览

| 项目 | 参数 |
|:--|:--|
| 产品数 | 3 |
| 每产品候选数 | 3（A_StrongHook / B_EmotionReversal / C_ProductFunction） |
| 总 Prompt 数 | 9 |
| 总生成视频数 | 9（每条 Prompt 生成 1 条，不评估同 Prompt 生成稳定性） |
| 品类覆盖 | 3（扩展到 30 条时补齐至 5 类） |
| 总周期 | 约 12 天 |

---

## 二、品类与产品选择

| 编号 | 品类 | PriceBand | 消费特征 |
|:--|:--|:--|:--|
| 品类 1 | 美妆 / 穿搭 / 食品（任选其一） | 中客单价 | 计划消费 |
| 品类 2 | 数码 / 工具 / 设备（任选其一） | 中高客单价 | 计划消费 |
| 品类 3 | 家居 / 生活方式 / 创意小物（任选其一） | 低客单价 | 冲动消费 |

**产品选择标准：** 有清晰产品图（短边 ≥400px）/ 卖点可画面化 / 使用场景明确 / 无合规风险 / 适配 15 秒。

---

## 三、三候选差异要求

| 差异项 | A_StrongHook | B_EmotionReversal | C_ProductFunction |
|:--|:--|:--|:--|
| Hook | 声音/视觉冲突 | 情绪张力 | 产品功能悬念 |
| 产品出场方式 | 视觉冲突中出现 | 情绪转折点出现 | 成为剧情转折条件 |
| 情绪弧线 | 惊讶→好奇→满足 | 好奇→紧张→释放 | 困惑→发现→满足 |
| CTA 策略 | 画面动作 CTA | 情绪落点 CTA | 产品使用结果 CTA |
| 结尾记忆点 | 反预期画面 | 情绪反转 | 产品改变故事走向 |

每个产品生成 A/B/C 三个候选，可选择一个 Winner 用于投放策略决策，但 Pilot 阶段仍渲染全部三个候选，用于比较不同候选类型的实际渲染表现。

---

## 四、渲染参数

| 参数 | 取值 |
|:--|:--|
| 分辨率 | 1080P |
| 画幅 | 由投放平台决定 |
| 时长 | 10-15 秒 |
| 声音输出 | AI 生成音频，包括环境音、动作声、音乐、短对白或语音；是否使用语音由 Prompt 决定，不强制口播 |
| 每条 Prompt 生成 | 1 条视频 |

---

## 五、标注流程（三步）

| 步骤 | 基于表 | 视图 | 执行者 | 内容 |
|:--|:--|:--|:--|:--|
| 独立标注 | Annotation | 独立标注视图 | Render Reviewer | 独立填写全部评分 |
| 分歧检查 | Annotation | 分歧检查视图 | Render Reviewer | HumanOverall 分歧 > 1 时触发复审 |
| 最终复审 | RenderResult | 最终复审视图 | PrimaryAnnotatorID | 聚合写入最终结果 |

单人项目：Annotation 9 条 → 直接写入 RenderResult。双人项目：Annotation 18 条 → 分歧检查 → 复审 → 写入 RenderResult。

**NoPost Audit 附加检查（记录在 Annotation Notes 中）：** 是否需要后期字幕 / 重新配音 / 补 Logo / 补价格URL / 剪辑节奏 / 修复画面瑕疵 / 重新生成。

---

## 六、投放参数

| 参数 | 取值 |
|:--|:--|
| 可投放条件 | HumanOverall ≥ 2 且 NoPostActual ≥ 2 |
| 每条视频平台数 | 1 个 |
| 测试预算 | 建议 ¥100-300 或等值外币，以平台最低预算为准 |
| 测试时长 | 24-48 小时 |
| 重点指标 | ThreeSecondViewRate / CompletionRate |

若可投放视频 < 6 条，Pilot 仍可完成，但必须记录不可投放原因并标记投放样本不足。

---

## 七、Pilot 时间线

```
Day 0:     准备（建表 / 建视图 / 选产品 / 备图）
Day 1-3:   Prompt 生成（9 条 Prompt + 评分 + VEL）
Day 4-5:   渲染生成（9 条视频 + 占位记录）
Day 5-7:   标注（独立标注 + 分歧检查 + 最终复审）
Day 7-10:  投放测试（可投放视频 × 1 平台）
Day 10-12: Dashboard 输出 + 校准判断 + 下轮建议
```

---

# 第四部分：执行 Checklist

---

## 阶段一：准备（Day 0）

| 编号 | 任务 | 产出 |
|:--|:--|:--|
| P-01 | 建 9 张表 | 表结构就绪 |
| P-02 | 建 18 个视图 | 视图就绪 |
| P-03 | 配角色权限 | 权限就绪 |
| P-04 | 选 3 个品类和 3 个产品 | Product Table 3 条记录 |
| P-05 | 准备产品图 | 每产品 ≥1 张高清图 |

## 阶段二：Prompt 生成（Day 1-3）

| 编号 | 任务 | 产出 |
|:--|:--|:--|
| P-06 | 产品 1 生成 3 个候选 | Prompt Table +3 |
| P-07 | 产品 1 评分 | PreScore Table +3 |
| P-08 | 产品 1 VEL 植入 | VEL Table +9~12 |
| P-09 | 产品 2 生成 3 个候选 | Prompt Table +3 |
| P-10 | 产品 2 评分 + VEL | PreScore +3 / VEL +9~12 |
| P-11 | 产品 3 生成 3 个候选 | Prompt Table +3 |
| P-12 | 产品 3 评分 + VEL | PreScore +3 / VEL +9~12 |

## 阶段三：渲染生成（Day 4-5）

| 编号 | 任务 | 产出 |
|:--|:--|:--|
| P-13 | 9 条 Prompt 提交渲染 | 9 条视频 |
| P-14 | 初步观察记录 | 临时备注，不写入 RenderResult 正式评分字段 |
| P-15 | 创建 RenderResult 占位记录 | 9 条（仅填写 VideoID / PromptID / VideoLink / RenderSuccess，其余留空待标注后聚合写入） |

**P-14/P-15 口径说明：** 渲染后对视频进行初步观察，记录 RenderSuccess（可在生成后立即判断）和其他临时观察备注。正式评分字段（VisualQuality / ProductVisibility / MotionAccuracy / FaceBodyStabilityScore / AudioMatchScore / TextQualityScore / NoPostActual / HumanOverall 等）必须由 Annotation 独立标注后，再由复审负责人聚合写入 RenderResult。RenderResult 不作为第一手独立标注入口。

## 阶段四：标注（Day 5-7）

| 编号 | 任务 | 产出 |
|:--|:--|:--|
| P-16 | Annotation 独立标注 | 9 条（单人）或 18 条（双人） |
| P-17 | 分歧检查 | 分歧 > 1 的记录标记 |
| P-18 | RenderResult 最终复审 | 9 条记录更新为完整标注 |
| P-19 | NoPost Audit 附加检查 | Notes 中 7 项检查 |
| P-20 | FailureReason 归类 | E1-E15 归类完整 |

## 阶段五：投放测试（Day 7-10）

| 编号 | 任务 | 产出 |
|:--|:--|:--|
| P-21 | 筛选可投放视频 | IsPublishable = "是" |
| P-22 | 提交投放 | 每条 1 平台 |
| P-23 | 记录投放指标 | AdResult Table |
| P-24 | 记录 AudienceSignal | AdResult 中填写 |

## 阶段六：Dashboard 与校准（Day 10-12）

| 编号 | 任务 | 产出 |
|:--|:--|:--|
| P-25 | 输出 Dashboard 15 项 | Pilot Run Report |
| P-26 | 失败类型 Top 5 | 统计列表 |
| P-27 | 识别校准需求 | CalibrationLog ≥1 条 |
| P-28 | 判断 Level 1 | 记录为样本不足，待扩展 |
| P-29 | 输出下轮建议 | 自由文本 |

---

## Pilot 完成标准

| 编号 | 标准 |
|:--|:--|
| 1 | 8 张表有记录（Series 可空） |
| 2 | 18 个视图全部可打开 |
| 3 | 9 条 Prompt 全部完成评分 |
| 4 | 9 条视频全部完成标注 |
| 5 | 目标 ≥6 条进入投放（若 <6 记录原因） |
| 6 | Dashboard 15 项全部输出 |
| 7 | CalibrationLog ≥1 条 |
| 8 | 所有失败样本有 FailureReason |
| 9 | 角色权限验证：团队项目验证角色权限隔离；个人项目记录为 Single-Operator Mode，验证全部视图可访问、全部字段可填写 |

---

## 扩展路径

| 阶段 | 产品 | 视频 | 品类 | 目标 |
|:--|:--|:--|:--|:--|
| Pilot | 3 | 9 | 3 | 流程验证 |
| 扩展第一轮 | +4（累计 7） | +12（累计 21） | +2（累计 5） | 品类覆盖达标 |
| 扩展第二轮 | +3（累计 10） | +9（累计 30） | 维持 5 | 样本量达标 |

---

# 附录

---

## A1. Error Taxonomy（E1-E15）

| 编号 | 失败类型 | 对应模块 |
|:--|:--|:--|
| E1 | 产品不清楚 | Q2 / ProductVisibility |
| E2 | 动作不符合 Prompt | Q5 / MotionAccuracy |
| E3 | 人脸或身体异常 | FaceBodyStabilityScore |
| E4 | 文字乱码或错误文字 | N1 / 铁律#5 |
| E5 | 音频不自然 | AudioMatchScore |
| E6 | 口型不同步 | N6 |
| E7 | 场景混乱 | Q5#2 / Q7#4 |
| E8 | 运镜失败 | 运镜指令体系 |
| E9 | 情绪弧不成立 | Q8 / EAD |
| E10 | 产品像硬广 | P_penalty / CriticPass#2 |
| E11 | CTA 不成立 | Q6 / NoPostGate |
| E12 | 需要后期才能理解 | NoPostGate / N4/N5 |
| E13 | VEL 无效或堆叠 | VEL 规则 / Naturalness |
| E14 | 画面质感不足 | Q3 / PRC |
| E15 | 生成成功但不适合投放 | HumanOverall / PostReady |

---

## A2. B5 Calibration Matrix（11 条合并版）

| # | 偏差模式 | 校准对象 | 校准动作 |
|:--|:--|:--|:--|
| 1 | PRC_Pre高但RenderSuccess低 | PRC / Q7 / KVS | 提高复杂物理、多主体、多场景、长对白风险权重 |
| 2 | PRC_Pre高但ProductVisibility低 | Q2 / PRC | 提高产品可见性要求，降低"产品暗示"得分 |
| 3 | NoPostGate通过但NoPostActual低 | NoPostRiskLoad / Cap Rules | 提高 N1、N4、N6、N8 权重，收紧 Cap Rules |
| 4 | Q1_Pre高但ThreeSecondViewRate低 | Q1#1-#3 | 收紧声音事件、视觉冲突、动作动词判定 |
| 5 | Q8_Pre高但CompletionRate低 | Q8#2 / Q8#5 / EAD | 收紧有效情绪段和前后情绪变化判定 |
| 6 | Q8_Pre高但RewatchRate低 | Q8#4 / Q4#5 | 收紧结尾反预期和复播点判定 |
| 7 | Q6_Pre高但CTR低 | 标题/评论/Bio/商品卡 | 重写投放资产，不改 Prompt 内核 |
| 8 | CTR高但CVR低 | 产品承诺/商品卡/落地页 | 检查卖点是否过度承诺 |
| 9 | VEL完整但VisualQuality低或无提升 | VEL 词库 | 减少 A/D 类抽象增强词，优先 C 类材质光影和 B 类角色生命 |
| 10 | AudioApplicable=Yes 且 AudioMatchScore 平均分 <1.3，或单条=0 | 音频描述规则 | 减少长对白，改为环境音、动作声、短对白；降低口型同步要求 |
| 11 | SCScore≥4 但 SeriesFollowRate<20% | SC 评估标准 | 校准角色一致性、世界观一致性、视觉风格一致性和集间悬念判定 |

---

## A3. 阶段性必填说明

| 阶段 | 必填表 | 说明 |
|:--|:--|:--|
| 创建 Prompt 时 | Product / Prompt / PreScore / VEL | 基础字段全部填写 |
| 渲染后 | RenderResult（占位：VideoID / PromptID / VideoLink / RenderSuccess）/ VEL_RenderResult | 占位记录 |
| 标注后 | Annotation / RenderResult（完整） | 全部评分字段聚合写入 |
| 投放后 | AdResult | 投放指标 |
| 系列激活时 | Series | 仅系列内容 |

---

## A4. 落地平台映射

| 字段类型 | Airtable | Notion | 飞书 |
|:--|:--|:--|:--|
| 单行文本 | Single line text | Text | 文本 |
| 长文本 | Long text | Text（多行） | 多行文本 |
| 单选 | Single select | Select | 单选 |
| 数值 | Number | Number | 数字 |
| 日期 | Date | Date | 日期 |
| 关联 | Link to record | Relation | 关联 |
| 公式 | Formula | Formula | 公式 |
| 聚合 | Rollup | Rollup | 聚合 |

---

## A5. 发布等级定义

| 等级 | 名称 | 条件 | 可以宣称 |
|:--|:--|:--|:--|
| Level 0 | Prompt Prototype | 只有 Prompt，无真实数据 | 结构化创意生成与专家先验评分系统 |
| Level 1 | Render Validated | ≥30 条生成，RenderSuccess≥80%，PRC 一致率≥70% | 经过渲染回测的创意编译系统 |
| Level 2 | NoPost Validated | DirectReady+LightEdit≥70%，Reject≤15%，NoPostGate 一致率≥70% | 经过 NoPost 验证的直接发布系统 |
| Level 3 | Ad Signal Validated | Q1/Q8 高低分组达到 MVP 区分度标准：高分组至少高于低分组 5 个百分点，或相对提升 ≥15%；样本不足时标记 Insufficient Sample | 具备投放信号区分能力的评分系统 |
| Level 4 | Calibration Ready | 至少一轮数据校准，所有 Kernel 修改有数据依据 | 经过数据校准的创意评估系统 |

---

## A6. NoPostActual 统一映射

| 数值 | 文本标签 | 含义 |
|:--|:--|:--|
| 3 | DirectReady | 无需后期可直接发布 |
| 2 | LightEdit | 主体可用，建议轻微剪辑 |
| 1 | NeedsPost | 必须后期处理才可发布 |
| 0 | Reject | 不可发布 |

所有 NoPost 视图、Dashboard 和公式均按该映射执行。

---

## A7. VideoLink 字段说明

VideoLink 为 v2.1-MVP 执行层必要字段，用于承接实际视频文件。v2.0.1 O1 原始 RenderResult Table 字段定义中不包含此字段。该字段不改变 v2.0.1 理论评分结构，仅解决执行层"视频文件入口缺失"问题，使 Render Reviewer 能够访问视频文件进行标注审查。后续不回写到 v2.0.1 理论规范，保持理论层与执行层的边界。

---

## A8. 视图数量说明

本文档定义 18 个核心视图为主结构。若平台不支持跨表 Kanban 或跨记录计算，需使用若干平台兜底筛选视图替代，此时实际视图数量可能超过 18。兜底视图不计入核心视图结构。

---

**HappyHorse CreativeOS v2.1-MVP — 表格落地版。**

**理论基础：** HappyHorse CreativeOS v2.0.1 系统规范定稿。

**归档状态：** 终稿通过。9 张表结构（含 9 项 Table Micro-Fix）、18 个核心视图（含 6 项 View Micro-Fix）、Pilot 执行指南（含 10 项 Pilot Micro-Fix + 5 项 Pilot Execution Micro-Fix + 7 项 Final Tabletop Micro-Fix）已全部合并。本文档作为 v2.1-MVP Pilot Run 的正式执行文档。后续不再修改理论结构、表结构主干和视图主干。下一阶段进入真实 Pilot Run。
