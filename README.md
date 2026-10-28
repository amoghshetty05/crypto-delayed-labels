# Safe Continual Adaptation of Cryptocurrency Fraud Detection Under Delayed Labels

## What this repo contains 
Reproduction of the base-paper pipeline on the Elliptic++ transaction dataset
(Elmougy & Liu, KDD 2023; builds on Weber et al., 2019):
- Data loaded and label-checked (4,545 illicit / 42,019 licit / 157,205 unknown)
- Time-ordered split: steps 1-34 train, 35-49 test, with a leakage test
- Static random-forest baseline (never updates)

## Results
| Metric | Paper (approx.) | Our reproduction |
|---|---|---|
| Precision (illicit) | ~97.5% | 97.1% |
| Recall (illicit) | ~71.9% | 72.0% |
| F1 (illicit) | - | 82.7% |
| PR-AUC | - | 0.790 |

Per time step, the static model collapses after the dark-market shutdown (step 43):

| Period | Illicit cases | Precision | Recall | F1 |
|---|---|---|---|---|
| Steps 35-42 | 914 | 0.986 | 0.850 | 0.913 |
| Steps 43-49 | 169 | 0.200 | 0.018 | 0.033 |

Note: very few labelled illicit cases exist after step 43, so single-step numbers there are noisy.

## Files
- `01_data_pipeline_and_static_baseline.ipynb` - the full pipeline
- `illicit_per_step.png`, `static_f1_per_step.png`, `per_step_metrics.csv` - results

## How to run
1. Download the Elliptic++ transaction files (`txs_features.csv`, `txs_classes.csv`,
   `txs_edgelist.csv`) from the official repo: https://github.com/git-disl/EllipticPlusPlus
2. Put them in a Google Drive folder and open the notebook in Colab.
3. Update the file paths in the first cells and run all cells.

## Next
Delayed-label experiment, contamination audit, canary set, update gate.
