# TII Operator Attention - 合成信号验证报告

> 生成时间: 2026-03-17
> 验证状态: ✅ 完成

---

## 📊 验证结果汇总

### 6类合成信号验证

| 信号类型 | FFT | HT | WF | LNO | I | 一致性 | 可解释性 |
|----------|-----|----|----|-----|---|--------|----------|
| 单频 (single_freq) | **0.690** | 0.091 | 0.127 | 0.054 | 0.038 | 0.999 | 0.368 |
| 高频 (high_freq) | **0.814** | 0.078 | 0.040 | 0.037 | 0.030 | 0.999 | 0.551 |
| 双频 (dual_freq) | **0.508** | 0.103 | 0.320 | 0.061 | 0.008 | 0.997 | 0.284 |
| 瞬态 (transient) | 0.081 | **0.619** | 0.147 | 0.065 | 0.088 | 0.996 | 0.270 |
| 噪声 (noisy) | 0.127 | 0.066 | **0.396** | **0.341** | 0.070 | 0.996 | 0.154 |
| 多尺度 (multi_scale) | 0.249 | 0.167 | **0.474** | 0.087 | 0.024 | 0.998 | 0.193 |

---

## 🎯 验证结论

### 1. 算子选择物理合理性 ✅

| 信号类型 | 预期主导算子 | 实际主导算子 | 验证结果 |
|----------|-------------|-------------|----------|
| 单频信号 | FFT | FFT (0.690) | ✅ 通过 |
| 高频信号 | FFT | FFT (0.814) | ✅ 通过 |
| 双频信号 | FFT+WF | FFT (0.508) + WF (0.320) | ✅ 通过 |
| 瞬态信号 | HT | HT (0.619) | ✅ 通过 |
| 噪声信号 | 稳定权重 | WF+LNO协同 | ✅ 通过 |
| 多尺度信号 | WF | WF (0.474) | ✅ 通过 |

### 2. 一致性指标 ✅

- **所有信号一致性 > 0.995**
- 表明算子注意力机制稳定可靠

### 3. 可解释性度量

- **最高可解释性**: 高频信号 (0.551) - FFT权重集中
- **最低可解释性**: 噪声信号 (0.154) - 权重分散

---

## 📝 论文可用结论

### Table: Synthetic Signal Validation Results

| Signal Type | Dominant Operator | Weight | Consistency | Interpretability |
|-------------|------------------|--------|-------------|------------------|
| Single-freq | FFT | 0.690 | 0.999 | 0.368 |
| High-freq | FFT | 0.814 | 0.999 | **0.551** |
| Dual-freq | FFT+WF | 0.828 | 0.997 | 0.284 |
| Transient | HT | 0.619 | 0.996 | 0.270 |
| Noisy | WF+LNO | 0.737 | 0.996 | 0.154 |
| Multi-scale | WF | 0.474 | 0.998 | 0.193 |

**Key Findings**:
1. FFT dominates for frequency-domain signals (single-freq: 0.690, high-freq: 0.814)
2. HT activates for transient signals (0.619)
3. WF responds to multi-scale features (0.474)
4. All signals achieve >0.995 consistency

---

## 📁 结果文件

```
TII_operator_attention/
├── results/
│   ├── synthetic_validation_results.json  ✅ 已保存
│   └── validation/
│       ├── theory_validation_report.md    ✅ 已有
│       └── quick_validation_results.json  ✅ 已有
└── figures/
    └── (待生成论文级图表)
```

---

## 🚀 下一步

1. ✅ 合成信号验证 - 完成
2. ⏳ 定理验证实验
3. ⏳ OAS/OSS/OCS度量
4. ⏳ 论文级图表生成

---

_生成: PHM研究总控智能体 | 2026-03-17_
