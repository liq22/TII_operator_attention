# Paper 07 Baseline And Ablation Matrix

Status date: 2026-05-11

This matrix binds the Paper 07 baseline and ablation surface to concrete
PHM-Vibench commands. It is not accepted submission evidence yet. The commands
must still be run on the accepted industrial datasets with the same split,
seed protocol, metrics, preprocessing, and local GPU metadata.

Machine-readable matrix: `submission_prep/baseline_ablation_matrix.yaml`

## Validation Performed

The following models were checked with `python -m scripts.config_inspect` from
the parent repository and resolved to registered model/task targets:

| ID | Target |
|---|---|
| B01/A01 | `X_model.NSN` |
| B02 | `X_model.Resnet` |
| B03 | `X_model.Sincnet` |
| B04 | `X_model.TFN` |
| B05 | `X_model.WKN` |
| B06 | `Transformer.ConvTransformer` |
| B07 | `CNN.AttentionCNN` |
| A02/A03/A04/A05/A06 | `X_model.NSN` with operator/temperature overrides |

The base Python environment still reports `ModuleNotFoundError("No module named
'pytorch_lightning'")` for trainer import during config inspection. Use
`LQ_signal` for executable runs. Config target resolution is not a substitute
for final training evidence.

## Required Next Evidence

1. Run every command in the YAML matrix with `CUDA_VISIBLE_DEVICES=0` or
   `CUDA_VISIBLE_DEVICES=1`.
2. Capture `run_meta.yaml`, `metrics.json`, stdout/stderr, seed, batch size,
   precision, runtime, GPU model, and OOM/failure reason.
3. Repeat under the accepted CWRU/XJTU or industrial protocol with enough
   seeds for mean, standard deviation, and confidence intervals.
4. Bind TimeMixer, SARAD, CATCH, and DADA to local representative commands or
   mark exact reproduction as `resource-blocked` under the 2x4090 budget.
5. Allow SOTA wording only after the proposed method beats all accepted
   baselines under the same protocol.
