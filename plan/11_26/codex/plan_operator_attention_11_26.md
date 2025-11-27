# Operator Attention Codex 执行计划（2024-11-26）

> 目标：完成从“严格算子注意力理论”到“在主仓库中可运行的 Operator Attention 模块”的闭环，并产出 TII 论文所需的实验与图表。  
> 范围：仅针对 `Paper/TII_operator_attention`，依赖主仓库模型与 Explainable_FD_Toolkit。

---

## 阶段 0：梳理理论文档与目标（Day 0–0.5）

**目标**：对当前理论推导与论文稿件的状态形成清晰认知。

- [ ] 阅读以下文件（可在 `doc/notes_11_26.md` 中记录要点）：  
  - `Paper/TII_operator_attention/Operator_Attention_Theory_Analysis.md`  
  - `Paper/TII_operator_attention/README.md`  
  - `Paper/TII_operator_attention/bare_jrnl_new_sample4.tex`（关注方法与实验部分结构）  
- [ ] 用简短要点回答：  
  - 理论推导已经覆盖哪些部分（定义、公式、复杂度）？  
  - 哪些部分还需要补充或整理？  
  - 最小实现版本的 Operator Attention 需要哪些关键组件？

产出：  
- 一份理论与工程 gap 的小结，指导后续优先级。

---

## 阶段 1：理论公式与符号系统精炼（Day 0.5–3）

**目标**：将 Operator Attention 的数学定义整理为清晰、可引用、与代码实现直接对应的版本。

- [ ] 在 `Operator_Attention_Theory_Analysis.md` 中：  
  - 明确写出：  
    - 算子集合与算子嵌入的定义；  
    - 注意力得分与输出计算公式；  
    - 门控与温度参数的作用；  
  - 添加符号表（变量、维度解释），减少阅读歧义。  
- [ ] 提供一个“简化版”公式版本，专门对应将要实现的第一个 Operator Attention 模块（例如单头、固定算子集合）。
- [ ] 把与标准 Self-Attention 的对比小结整理成一个独立小节，便于 TII 论文引用。

产出：  
- 一份结构清晰、适合直接引用到 LaTeX 的理论说明文档。

---

## 阶段 2：在主仓库模型中的最小实现（Day 4–8）

**目标**：在至少一个主仓库模型（如 TSPN）中嵌入 Operator Attention 的最小工作版本。

### 2.1 模块代码实现

- [ ] 在主仓库 `model/` 下新建一个模块文件（如 `operator_attention.py`）：  
  - 实现简化版 Operator Attention 层：  
    - 接收输入特征 + 算子集合（或其嵌入）；  
    - 输出加权后的算子组合结果。  
- [ ] 提供可配置参数（算子数量、嵌入维度、是否使用门控等）。

### 2.2 集成到模型

- [ ] 在 TSPN 或相关模型中选定一层，将原有的简单算子加权替换/并联为 Operator Attention 版本（保持可切换开关）；  
- [ ] 增加配置文件（如 `configs/THU_018/config_TSPN_opatt.yaml`），包含：  
  - 是否启用 Operator Attention；  
  - Operator Attention 的关键超参数。

### 2.3 最小实验脚本

- [ ] 在主仓库或本子目录下新增脚本（如 `scripts/run_opatt_minimal_demo.py`）：  
  - 在小规模数据上训练 1–2 个 epoch，验证：  
    - 模型可正常前向/反向；  
    - 注意力权重数值合理（无 NaN/爆炸）。  

产出：  
- 一个嵌入 TSPN 的最小 Operator Attention 版本 + 基本训练日志。

---

## 阶段 3：对比实验与可解释性分析（Day 9–16）

**目标**：构建三组对照：无注意力 vs Self-Attention vs Operator Attention，并分析算子级解释性。

### 3.1 性能与复杂度对比

- [ ] 在至少 1 个数据集上，比较三种模型：  
  - baseline TSPN（无注意力）；  
  - 带 Self-Attention 的版本（位置/通道）；  
  - 带 Operator Attention 的版本。  
- [ ] 收集指标：Accuracy、F1、推理时间、参数量、显存占用等。

### 3.2 算子注意力可解释性分析

- [ ] 为 Operator Attention 版本：  
  - 记录不同故障类型/工况下的算子权重分布；  
  - 统计稀疏度、一致性、物理一致性评分（可用简单规则或专家先验）。  
- [ ] 对比 Self-Attention：说明“关注算子 vs 关注位置/通道”的差异。

产出：  
- 一套用于论文主表的性能/复杂度/可解释性数据；  
- 1–2 个关键图（算子权重热力图、随工况变化曲线）。

---

## 阶段 4：TII 论文图表与文字整合（Day 17–24）

**目标**：将理论与实验结果落地到 TII 论文稿中。

- [ ] 在 `bare_jrnl_new_sample4.tex` 中补充/更新：  
  - 方法部分：插入整理后的 Operator Attention 数学定义；  
  - 实验部分：插入性能对比表与算子注意力可视化图；  
  - 讨论部分：总结与 Self-Attention 和传统算子加权的差异。  
- [ ] 确保所有图表文件（在 `figs/` 下）都与 LaTeX 引用一致，路径正确。

产出：  
- 一版结构完整、理论与实验对应清晰的 TII 论文草稿。

---

## 阶段 5：与 MoE / 1D-2D / NeSy 的扩展联系（Day 25+）

**目标**：探索 Operator Attention 与其他方法层/理论层方法的协同。

- [ ] 与 MoE_explainable 联动：  
  - 探讨“算子级 attention + 路径级 MoE”的组合，是否能提供更丰富的解释；  
  - 可以先做概念性讨论或小规模实验。  
- [ ] 与 1D-2D 融合联动：  
  - 研究在多模态场景下，对 1D 和 2D 各自/联合施加算子注意力的效果。  
- [ ] 与 Neuralsymbolic-XFD 对齐：  
  - 将 Operator Attention 中的算子看作符号层的一部分，讨论其在框架中的位置与性质。

产出：  
- 若干跨方法的初步思路或小实验结果，可作为未来工作或扩展论文内容。

---

## 总结：后续 Codex/Agent 使用建议

1. 想“先让算子注意力跑起来” → 优先完成 **阶段 1–2** 中的简化公式和最小实现。  
2. 想“形成有说服力的实验对比” → 在有实现基础上重点推进 **阶段 3**。  
3. 想“推动 TII 论文定稿” → 使用 **阶段 4** 的任务对齐 LaTeX 与图表。  
4. 想“与 MoE/1D-2D/NeSy 协同扩展” → 在论文主线稳定后，再考虑 **阶段 5**。  

