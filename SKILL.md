---
name: medxpert-ai-samd-reg-skill
description: 医疗AI/SaMD（软件即医疗器械）注册路径与特殊要求。输入AI器械的功能+风险等级，输出分类判定+特殊文档要求+PCCP/GMLP准备清单。Use for：AI医疗器械注册、SaMD分类、大模型医疗应用、算法变更管理、GMLP合规。Do NOT use for：普通硬件器械注册（用medxpert-reg-path-skill）、临床评价（用medxpert-clinical-eval-skill）。触发词：医疗AI、SaMD、AI医疗器械、大模型医疗、GMLP、PCCP、算法变更、独立软件。
---

# MedXpert AI SaMD Reg Skill · 医疗AI注册专用

> 这是MedXpert Skill全家桶的**第一个垂直品类Skill**——专门针对AI/SaMD医疗器械。
> 前四个是通用注册流程，这个是AI这个细分品类的特殊要求。

---

## 为什么单独做一个AI Skill？

医疗AI注册和普通器械**完全不一样**：
- 有特殊的分类框架（IMDRF SaMD分级）
- 有特殊的文档要求（GMLP、PCCP）
- 有特殊的临床验证要求（算法性能数据集）
- 有特殊的变更管理（算法更新要不要重新注册？）

普通注册Skill覆盖不了这些特殊要求。

---

## 这个 Skill 做什么

输入：你的AI软件是干什么的、给谁用、风险多大
输出：
1. SaMD分类判定（I/II/III/IV级）
2. 注册路径建议（510(k)/De Novo/PMA，还是NMPA三类）
3. AI特殊文档清单：GMLP、PCCP、算法描述、数据集说明
4. 发补高风险点预警

---

## 何时使用

### ✅ 合适的场景

- 做AI辅助诊断软件（比如影像AI）
- 做大模型医疗应用（比如辅助问诊、病历生成）
- 做SaMD独立软件（不是硬件附带的）
- 算法要更新，不知道要不要重新注册

### ❌ 不合适的场景

- 普通硬件器械（用①路径决策）
- 硬件附带的简单软件（不是独立SaMD）
- 临床评价怎么写（用④临床评价Skill）

---

## 工作流

### Step 1 · 先确认这是不是SaMD

先判断：
- 这个软件是不是独立运行的？（不是硬件内置的）
- 它是不是用于医疗目的？（诊断/治疗/监测/预测）
- 如果不是独立SaMD，那就是普通软件，走普通注册路径

### Step 2 · SaMD分类判定

读 `references/samd-classification.md`，按IMDRF框架分：
- 按**医疗情况**：紧急/非紧急/严重/非严重
- 按**决策影响**：治疗驱动/治疗管理/临床管理/驱动临床管理
- 输出：SaMD等级 I/II/III/IV

### Step 3 · 注册路径建议

根据分类，给出对应市场的路径：
- 美国FDA：510(k) / De Novo / PMA
- 欧盟MDR：Class IIa / IIb / III
- 中国NMPA：二类 / 三类

### Step 4 · AI特殊文档清单

列出普通器械不需要、但AI必须要的东西：
- GMLP（良好机器学习实践）合规报告
- PCCP（预定变更控制计划）——如果算法要持续更新
- 算法描述文档（模型架构、训练方法、验证策略）
- 数据集说明（训练集/测试集分布、偏倚分析）

### Step 5 · 发补高风险预警

告诉用户：AI注册最容易被发补的点在哪里：
- 数据集代表性不够
- 算法性能指标不达标
- PCCP写得不清楚
- 没有做真实世界验证

---

## 硬规则

### 🚫 P0级禁令

1. **不许把AI器械按普通器械注册路径套**——AI有特殊要求，必须单独评估
2. **不许跳过数据集偏倚分析**——医疗AI最容易翻车的地方就是数据集偏倚
3. **PCCP必须写清楚**——算法能改什么、不能改什么，必须明确
4. **不许承诺"算法更新不需要重新注册"**——要看FDA/NMPA怎么批的

---

## 资源文件导览

```
medxpert-ai-samd-reg-skill/
├── SKILL.md
├── references/
│   ├── samd-classification.md      ← SaMD分类判定（IMDRF框架）
│   ├── gmlp-pccp-checklist.md      ← GMLP + PCCP自查清单
│   └── deficiency-highlights.md    ← AI器械注册高发补点
└── assets/
    └── examples/
        └── example-ai-imaging-dx.md  ← AI影像辅助诊断示例
```

---

> 🛡️ 本Skill是MedXpert LGD体系的一环：有籍有证有门禁。
> 通用流程Skill：[①路径决策](../medxpert-reg-path-skill/) · [②申报前自查](../medxpert-pre-submission-check-skill/) · [③发补回复](../medxpert-deficiency-reply-skill/) · [④临床评价](../medxpert-clinical-eval-skill/)
