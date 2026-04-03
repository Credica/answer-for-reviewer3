# Supplementary Material for Reviewer3
---

<table>
  <thead>
    <tr>
      <th>Domain</th>
      <th>Tasks</th>
      <th># Tasks</th>
      <th>Simulator</th>
      <th>State Dim</th>
      <th>Action Dim</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Locomotion</td>
      <td>hopper / halfcheetah / walker2d (medium-expert-v2)</td>
      <td>3</td>
      <td>MuJoCo</td>
      <td>11–17</td>
      <td>3–6</td>
    </tr>
    <tr>
      <td>Dexterous</td>
      <td>pen-cloned/human-v1, door-cloned/human-v1</td>
      <td>4</td>
      <td>Adroit</td>
      <td>45</td>
      <td>24–28</td>
    </tr>
    <tr>
      <td>Kitchen</td>
      <td>kitchen-partial-v0, kitchen-complete-v0</td>
      <td>2</td>
      <td>Franka Kitchen</td>
      <td>60</td>
      <td>9</td>
    </tr>
    <tr>
      <td>Navigation</td>
      <td>antmaze-umaze-v0</td>
      <td>1</td>
      <td>AntMaze</td>
      <td>29</td>
      <td>8</td>
    </tr>
    <tr>
      <td><strong>Note</strong></td>
      <td colspan="5">Compared to OCW, D4RL-CL-10 poses three additional challenges: <strong>heterogeneous state/action spaces</strong> (state dim spans 11→60), <strong>diverse simulators</strong> (4 physically distinct engines vs. OCW's unified MuJoCo).</td>
    </tr>
  </tbody>
</table>

---










## Table 1: Task Order Robustness — Full Results (OCW-10, 3 Seeds)

| Order | Task Sequence (T1 → T10)                                                                                                                                  |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0     | hammer-v2, push-wall-v2, faucet-close-v2, push-back-v2, stick-pull-v2, handle-press-side-v2, push-v2, shelf-place-v2, window-close-v2, peg-unplug-side-v2 |
| 1     | push-v2, window-close-v2, peg-unplug-side-v2, shelf-place-v2, handle-press-side-v2, push-back-v2, hammer-v2, stick-pull-v2, push-wall-v2, faucet-close-v2 |
| 2     | handle-press-side-v2, peg-unplug-side-v2, push-back-v2, stick-pull-v2, push-v2, shelf-place-v2, faucet-close-v2, window-close-v2, push-wall-v2, hammer-v2 |
| 3     | push-wall-v2, handle-press-side-v2, push-v2, hammer-v2, peg-unplug-side-v2, stick-pull-v2, shelf-place-v2, faucet-close-v2, window-close-v2, push-back-v2 |



| Category | Method     | Order 0       | Order 1       | Order 2       | Order 3       | Avg      |
| -------- | ---------- | ------------- | ------------- | ------------- | ------------- | -------- |
| Reg      | L2         | 0.29±0.06     | 0.20±0.03     | 0.23±0.05     | 0.29±0.05     | 0.25     |
|          | EWC        | 0.16±0.02     | 0.12±0.02     | 0.11±0.02     | 0.15±0.03     | 0.13     |
|          | MAS        | 0.29±0.04     | 0.17±0.01     | 0.16±0.06     | 0.20±0.04     | 0.21     |
|          | LwF        | 0.21±0.04     | 0.15±0.04     | 0.18±0.05     | 0.19±0.00     | 0.18     |
|          | RWalk      | 0.26±0.03     | 0.17±0.01     | 0.25±0.02     | 0.20±0.01     | 0.22     |
|          | VCL        | 0.14±0.03     | 0.11±0.01     | 0.11±0.01     | 0.12±0.03     | 0.12     |
|          | Finetuning | 0.11±0.03     | 0.12±0.02     | 0.15±0.06     | 0.12±0.03     | 0.12     |
| Struc    | LoRA       | 0.54±0.03     | 0.47±0.02     | 0.35±0.03     | 0.43±0.05     | 0.45     |
|          | PackNet    | 0.64±0.06     | 0.67±0.01     | 0.65±0.03     | 0.65±0.04     | 0.65     |
|          | Grow       | 0.60±0.06     | 0.54±0.05     | 0.43±0.01     | 0.51±0.05     | 0.52     |
| Reh      | PM         | 0.26±0.01     | 0.26±0.10     | 0.25±0.03     | 0.27±0.01     | 0.26     |
|          | A-GEM      | 0.12±0.04     | 0.12±0.02     | 0.11±0.01     | 0.15±0.04     | 0.13     |
| **Ours** | **HTAC**   | **0.72±0.04** | **0.72±0.02** | **0.70±0.03** | **0.69±0.03** | **0.71** |




---

## Table 2: FWT Decomposition on OCW-20 (HTAC, 3 Seeds)
| Component       | Avg.            | Interpretation                               |
| --------------- | --------------- | -------------------------------------------- |
| Tasks 1→10 FWT  | 0.018±0.019     | Transfer to genuinely novel tasks            |
| Tasks 11→20 FWT | **0.700±0.016** | Automatic reactivation of historical experts |
| **Overall FWT** | **0.39±0.04**   | Composite of both capabilities               |

---

## Table 3: Threshold θ Sensitivity Analysis (OCW-20, 3 Seeds)


| Metric | θ=0.5     | θ=0.6     | θ=0.7      | **θ=0.8 (paper)** | θ=0.9      | θ=1.0      |
| ------ | --------- | --------- | ---------- | ----------------- | ---------- | ---------- |
| P ↑    | 0.67±0.05 | 0.70±0.04 | 0.71±0.05  | **0.77±0.01**     | 0.74±0.04  | 0.72±0.03  |
| F ↓    | 0.01±0.02 | 0.00±0.02 | −0.00±0.03 | **−0.04±0.02**    | −0.02±0.02 | −0.01±0.03 |
| FWT ↑  | 0.33±0.03 | 0.35±0.05 | 0.35±0.05  | **0.39±0.04**     | 0.37±0.03  | 0.37±0.03  |


---

## Table 4: Domain Number D Ablation (OCW-10, 3 Seeds)


| D ( Domains) | P ↑           | F ↓            | FWT ↑         |
| ------------- | ------------- | -------------- | ------------- |
| 1             | 0.64±0.02     | −0.00±0.05     | 0.00±0.01     |
| 2             | 0.59±0.09     | 0.01±0.01      | 0.02±0.01     |
| 3             | 0.63±0.08     | 0.03±0.02      | 0.01±0.02     |
| **4 (paper)** | **0.72±0.08** | **−0.02±0.04** | **0.06±0.10** |
| 5             | 0.59±0.06     | 0.06±0.02      | 0.00±0.00     |
| 6             | 0.67±0.02     | −0.02±0.03     | 0.00±0.00     |



---

## Table 5: HTAC Parameter Breakdown (CW-10)


| Component                            | Parameters | Notes                              |
| ------------------------------------ | ---------- | ---------------------------------- |
| Backbone (Shared)                    | 7.33M      | Shared across all tasks            |
| S-BERT (Frozen)                      | 22.71M     | Pre-trained LM, **not CL-related** |
| Domain Prototypes                    | 1.5K       | D=4 prototype vectors              |
| Proj Networks                        | 328.7K     | Task desc → prototype space        |
| Composition Modules (W_Q/W_K/Fusion) | 3.94M      | Attention-based composition        |
| Domain Experts                       | 6.31M      | 4 domain-level experts             |
| Task Experts                         | 12.62M     | Per-task expert heads              |
| Per-Task Adapters                    | 2.38M      | Lightweight task-specific adapt    |
| Prediction Heads                     | 10.3K      | Output layers                      |
| **Total**                            | **55.62M** |                                    |
| **CL-related only (excl. S-BERT)**   | **32.91M** |                                    |


**Baseline Comparison (OCW-10)**


| Method              | Total Params | P (CW-10) | F     | FWT   | P/M（P / Total Params (M)）   |
| ------------------- | ------------ | --------- | ----- | ----- | ----- |
| Finetuning          | 5.02M        | 0.12      | 0.73  | 0.02  | 0.024 |
| L2                  | 5.02M        | 0.23      | 0.00  | −0.01 | 0.046 |
| EWC                 | 5.02M        | 0.11      | 0.76  | 0.01  | 0.022 |
| MAS                 | 5.02M        | 0.25      | 0.44  | −0.02 | 0.050 |
| LwF                 | 5.02M        | 0.14      | 0.65  | 0.02  | 0.028 |
| RWalk               | 5.02M        | 0.33      | −0.07 | −0.02 | 0.066 |
| VCL                 | 5.02M        | 0.08      | 0.74  | 0.00  | 0.016 |
| A-GEM               | 5.02M        | 0.12      | 0.73  | −0.02 | 0.024 |
| PackNet             | 5.02M        | 0.69      | 0.05  | −0.02 | 0.137 |
| Perfect Memory      | 5.02M        | 0.28      | 0.55  | −0.02 | 0.056 |
| LoRA                | 5.56M        | 0.48      | 0.01  | −0.03 | 0.086 |
| Grow                | 8.81M        | 0.67      | −0.05 | 0.00  | 0.076 |
| **HTAC (ours)**     | **55.62M**   | **0.60**  | 0.06  | 0.09  | 0.011 |
| HTAC (excl. S-BERT) | 32.91M       | **0.60**  | 0.06  | 0.09  | 0.018 |


