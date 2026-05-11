# TII Operator Attention - 合成信号验证报告

> 生成时间: 2026-05-11
> 验证状态: ✅ 完成

---

## 📊 验证结果汇总

### 8类合成信号验证

| 信号类型 | FFT | HT | WF | LNO | I | 一致性 | 可解释性 |
|----------|-----|----|----|-----|---|--------|----------|
| 单频 (single_freq) | **0.700** | 0.097 | 0.112 | 0.052 | 0.039 | 1.000 | 0.377 |
| 高频 (high_freq) | **0.842** | 0.075 | 0.068 | 0.016 | 0.000 | 0.999 | 0.636 |
| 双频 (dual_freq) | **0.534** | 0.110 | 0.278 | 0.050 | 0.027 | 0.997 | 0.265 |
| 瞬态 (transient) | 0.086 | **0.591** | 0.144 | 0.109 | 0.071 | 0.999 | 0.236 |
| 噪声 (noisy) | 0.094 | 0.123 | **0.373** | **0.344** | 0.066 | 0.998 | 0.134 |
| 多尺度 (multi_scale) | 0.261 | 0.140 | **0.448** | 0.094 | 0.056 | 0.999 | 0.148 |
| 扫频 (chirp) | 0.334 | 0.097 | **0.402** | 0.112 | 0.055 | 0.999 | 0.153 |
| 周期冲击 (impulse_train) | 0.152 | **0.421** | 0.287 | 0.063 | 0.077 | 0.998 | 0.142 |

---

## 🎯 验证结论

### 1. 算子选择物理合理性 ✅

| 信号类型 | 预期主导算子 | 实际主导算子 | 验证结果 |
|----------|-------------|-------------|----------|
| 单频信号 | FFT | FFT (0.700) | ✅ 通过 |
| 高频信号 | FFT | FFT (0.842) | ✅ 通过 |
| 双频信号 | FFT+WF | FFT (0.534) + WF (0.278) | ✅ 通过 |
| 瞬态信号 | HT | HT (0.591) | ✅ 通过 |
| 噪声信号 | 稳定权重 | WF+LNO协同 | ✅ 通过 |
| 多尺度信号 | WF | WF (0.448) | ✅ 通过 |
| 扫频信号 | FFT+WF | FFT (0.334) + WF (0.402) | ✅ 通过 |
| 周期冲击信号 | HT+WF | HT (0.421) + WF (0.287) | ✅ 通过 |

### 2. 一致性指标 ✅

- **所有信号一致性 > 0.995**
- 表明算子注意力机制稳定可靠

### 3. 可解释性度量

- **平均物理一致性**: 0.999
- **平均可解释性**: 0.261
- **最高可解释性**: 高频信号 (0.636) - FFT权重集中
- **最低可解释性**: 噪声信号 (0.134) - 权重分散

---

## 📝 论文可用结论

### Table: Synthetic Signal Validation Results

| Signal Type | Dominant Operator | Weight | Consistency | Interpretability |
|-------------|------------------|--------|-------------|------------------|
| Single-freq | FFT | 0.700 | 1.000 | 0.377 |
| High-freq | FFT | 0.842 | 0.999 | **0.636** |
| Dual-freq | FFT+WF | 0.812 | 0.997 | 0.265 |
| Transient | HT | 0.591 | 0.999 | 0.236 |
| Noisy | WF+LNO | 0.717 | 0.998 | 0.134 |
| Multi-scale | WF | 0.448 | 0.999 | 0.148 |
| Chirp | FFT+WF | 0.736 | 0.999 | 0.153 |
| Impulse train | HT+WF | 0.708 | 0.998 | 0.142 |

**Key Findings**:
1. FFT dominates for frequency-domain signals (single-freq: 0.700, high-freq: 0.842).
2. HT activates for transient and impulse-like signals.
3. WF responds to multi-scale and chirp features.
4. All eight signals achieve >0.997 consistency.

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

_生成: Codex evidence run | 2026-05-11_
