# IEEE Transactions Readiness Evidence

Status date: 2026-05-11

This note is the strict-reviewer gate for the current TII operator-attention
package. It records runnable evidence and blocks any unsupported submission or
SOTA claim.

## Canonical Package

- Canonical manuscript entrypoint: `manuscript/final_tex/main.tex`
- Source manuscript consumed by canonical entrypoint: `bare_jrnl_new_sample4.tex`
- Existing PDF: `bare_jrnl_new_sample4.pdf`
- Parent-facing reproduction contract: `VIBENCH.md`
- Minimal PHM-Vibench config: `configs/vibench/min.yaml`
- Main synthetic validation entrypoint: `python code/synthetic_verification.py`

## Verified Commands

Synthetic operator-selection validation:

```bash
python code/synthetic_verification.py
```

Result on 2026-05-11:

- Exit code: 0
- Signal classes covered: 8
- Mean physics consistency: 0.999
- Mean explainability score: 0.261
- Output figures:
  - `figures/synthetic_signals.png`
  - `figures/operator_weights_heatmap.png`
  - `figures/explainability_comparison.png`
- Output data:
  - `results/synthetic_validation_results.json`
  - `doc/synthetic_verification_report.md`

Minimal PHM-Vibench smoke run:

```bash
eval "$(conda shell.bash hook)"
conda activate LQ_signal
CUDA_VISIBLE_DEVICES=0 python main.py --config paper/UXFD_paper/TII_operator_attention/configs/vibench/min.yaml --override trainer.num_epochs=1
```

Result on 2026-05-11:

- Exit code: 0 in `LQ_signal`
- Base environment blocker: `ModuleNotFoundError("No module named 'pytorch_lightning'")`
- Runtime device: CPU fallback; `CUDA_VISIBLE_DEVICES=0` was set, but PyTorch reported GPU unavailable in this sandbox
- Dummy-data output root:
  `results/uxfd/pilot/TII_operator_attention/metadata_dummy.csv/M_NSN/`
- Representative test metric from the run:
  `test_loss=0.7221537828445435`, `test_acc_Dummy_Data=0.0`

The smoke run proves the entrypoint wiring only. It does not prove industrial
accuracy, SOTA performance, or submission readiness.

Canonical TeX compile gate:

```bash
pdflatex -interaction=nonstopmode manuscript/final_tex/main.tex
```

Result on 2026-05-11:

- Exit code: 0
- Output: `main.pdf`
- Scope: compileability of the normalized IEEE entrypoint only; the manuscript
  still needs evidence-table updates before submission.

## Current Gate Status

| Gate | Status | Evidence or blocker |
|---|---|---|
| Canonical TeX entrypoint | partial pass | `manuscript/final_tex/main.tex` compiles from the submodule root and consumes `bare_jrnl_new_sample4.tex`; evidence tables still require command-backed updates before submission. |
| Synthetic validation | partial pass | Script runs, writes submodule-local artifacts, and covers 8 signal classes; this satisfies the synthetic signal-count gate but remains simulated operator-selection evidence only. |
| Industrial runnable entrypoint | partial | `configs/vibench/min.yaml` runs as dummy-data smoke in `LQ_signal`; no industrial protocol proof yet. |
| 6+ baseline suite | blocked | Required baselines are declared in the parent goal, but same-protocol runs and artifacts are not present. |
| Ablation suite | blocked | Existing figures mention ablation, but accepted artifact mapping for remove-operator-attention, sparse/L1, physics consistency, operator subset, and temperature/sparsity sensitivity is missing. |
| TOP recent-work representative | blocked | Parent goal requires TimeMixer, SARAD, CATCH, and DADA representatives; no local same-protocol command/log/artifact mapping exists yet. |
| SOTA diagnosis claim | blocked | No same-protocol industrial-data evidence beats the declared baselines. Use theory/interpretable-mechanism wording only. |
| Rejection-recovery trace | partial | `revision/review_response_plan.md` exists; it still needs command-backed evidence links. |

## Next Execution Milestone

1. Add a paper-local baseline matrix with at least six commands:
   no operator attention, ResNet1D, SincNet, TFN, WKN, PatchTST or
   ConvTransformer, and feature/self-attention using the same backbone.
2. Add ablation commands for operator removal, sparse/L1 removal, physics
   consistency removal, operator subset sweep, feature/self-attention
   comparison, and sparsity/temperature sensitivity.
3. Bind the TOP recent-work representatives to local commands or explicitly
   mark exact reproduction as `resource-blocked` under the two RTX 4090 budget.
4. Update the normalized manuscript package after the evidence tables are
   generated.
