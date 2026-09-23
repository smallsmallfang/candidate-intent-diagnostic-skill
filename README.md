# Candidate Intent Diagnostic

> 一个帮助 HR / Recruiter 识别、诊断候选人真实意愿，并决定下一步处理方式的 AI Skill。

## 为什么做这个 Skill？

招聘过程中，一个候选人说：

> “我不考虑了。”

并不一定意味着：

> “我对你们公司完全没兴趣。”

他可能是在表达：

- 这个岗位目前的设计我不能接受；
- 风险太高；
- 权责不匹配；
- 薪资条件不满足；
- 我有兴趣，但还没有足够的信息做决定；
- 我愿意继续谈，但需要你们解决某个关键问题；
- 我不接受这次机会，但愿意保留关系。

因此，招聘沟通真正需要解决的问题不是简单判断：

**“候选人要不要来？”**

而是：

**“候选人为什么现在不来？什么条件可能改变这个决定？”**

这个 Skill 尝试把这件事情结构化。

---

## 核心能力

`candidate-intent-diagnostic` 主要完成四件事：

```text
招聘沟通
   ↓
提取候选人信号
   ↓
诊断候选人意愿与阻碍
   ↓
判断下一步 HR 动作
```

重点区分：

| 类型 | 含义 |
|---|---|
| Genuine Reject | 真正拒绝 |
| Conditional Interest | 条件性兴趣 |
| Risk-Blocked Interest | 有兴趣，但风险阻断 |
| Role-Design Blocked | 岗位设计本身存在问题 |
| Compensation / Condition Blocked | 薪资或工作条件阻断 |
| Negotiation | 谈判 |
| Relationship-Preserving Reject | 拒绝当前机会，但愿意保留关系 |

一个候选人可以同时拥有多个标签。

例如：

```text
High Interest
+
High Risk Sensitivity
+
Role-Design Concern
+
Relationship Preserving
```

这比简单标记为“候选人拒绝 Offer”更有信息价值。

---

## 核心判断模型

Skill 从六个维度观察候选人：

```text
Interest       对公司 / 工作本身的兴趣
Fit            岗位与候选人需求的匹配程度
Conditions     薪资、地点、工作方式等条件
Risk           候选人感知到的职业风险
Commitment     候选人为机会投入了多少沟通成本
Relationship   候选人是否愿意保留与招聘方的关系
```

最终回答：

> 候选人到底是在拒绝“这个机会”，还是拒绝“当前版本的这个机会”？

---

## 一个重要原则

### 不要根据候选人的一句话判断意愿。

例如：

> “我再考虑一下。”

本身的信息量非常低。

需要结合：

- 候选人之前说了什么；
- 是否持续追问；
- 是否提出具体条件；
- 是否愿意继续沟通；
- 是否解释拒绝原因；
- 是否提出替代方案；
- 是否仍然愿意和 Recruiter / Hiring Manager 沟通。

因此 Skill 会综合**语言信号 + 行为信号 + 决策一致性 + 持续沟通意愿**进行判断。

---

## 输出内容

Skill 会输出结构化诊断：

```text
Candidate Intent Diagnosis

1. Overall Assessment
2. Interest Profile
3. Main Blockers
4. Key Signals
5. Candidate Decision Model
6. Recommended Recruiter Action
7. Next Best Question
8. Escalation
```

例如：

```text
Primary Intent:
Risk-Blocked Interest

Secondary Intent:
Role-Design Blocked

Confidence:
Medium-High

Recommended Action:
不要继续重复介绍公司愿景。
应该由 Hiring Manager 明确：
- 汇报关系
- 决策权限
- 资源
- 3/6个月成功标准
```

---

## Recruiter 应该得到什么？

这个 Skill 不负责“帮 HR 把候选人忽悠进来”。

它更关注：

### 1. Close

候选人是真拒绝。

→ 尊重决定，结束流程。

### 2. Clarify

候选人缺信息。

→ 继续澄清。

### 3. Negotiate

候选人有兴趣，但存在可谈条件。

→ 进入谈判。

### 4. Escalate

问题属于岗位设计、组织结构或权限。

→ 找 Hiring Manager / Business Leader 解决。

### 5. Preserve

候选人拒绝当前机会，但关系仍然很好。

→ 保留人才关系。

### 6. Revisit

条件未来可能变化。

→ 进入 Talent Pool，未来重新接触。

---

## 使用方式

将 `SKILL.md` 放入你的 Skill 目录中，然后向 AI 提供招聘沟通内容，例如：

```text
请分析下面这段 Recruiter 和候选人的聊天：

[粘贴聊天记录]

按照 Candidate Intent Diagnostic 进行分析。
```

也可以直接提出：

```text
这个候选人是真的拒绝，还是条件性拒绝？
```

或者：

```text
这个候选人到底卡在哪里？
```

或者：

```text
作为 Recruiter，我下一步应该问什么？
```

---

## 项目结构

当前 1.0 版本保持轻量：

```text
candidate-intent-diagnostic/
│
├── README.md
└── SKILL.md
```

后续可以逐步扩展：

```text
candidate-intent-diagnostic/
│
├── README.md
├── SKILL.md
│
├── references/
│   ├── intent-taxonomy.md
│   ├── signal-library.md
│   ├── diagnostic-tree.md
│   ├── recruiter-actions.md
│   └── examples.md
│
└── examples/
    ├── genuine-reject.md
    ├── conditional-interest.md
    ├── role-design-blocked.md
    ├── compensation-blocked.md
    └── anonymized-cases/
```

---

## 1.0 Roadmap

当前版本重点是建立基础诊断框架。

后续可以从真实招聘案例中迭代：

### V1.1
增加更多真实案例与边界案例。

### V1.2
增加更细的语言 / 行为 Signal Library。

### V1.3
增加 Candidate Decision Tree。

### V2.0
增加不同候选人类型、不同招聘阶段的诊断模型：

```text
初次接触
↓
面试
↓
业务沟通
↓
Offer
↓
谈薪
↓
拒绝
↓
Offer 后反悔
```

---

## 核心理念

> **不要只问：候选人想不想来。**

更应该问：

> **候选人愿意接受什么版本的这个机会？**

以及：

> **什么阻碍了那个版本的机会在今天成立？**

当 HR 能回答这两个问题时，招聘就不再只是“推进候选人”，而开始真正理解候选人的决策模型。

---

## License

暂定采用 MIT License。

本项目用于探索 AI 在招聘沟通、候选人意愿诊断与招聘决策辅助中的应用。

AI 输出应作为辅助信息，不应替代 Recruiter、Hiring Manager 对候选人的实际判断。
