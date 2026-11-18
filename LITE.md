# TabArena-Lite evaluation of checkpoint 448

The single fixed configuration completed all 51 first outer splits on one NVIDIA GB10. Each fit used the official 8-fold, 1-repeat validation protocol and full refit. The GPU allocation was one device, with four CPUs per model, FP32 inference, one native preprocessing member, and a 512-row support cap. The weights stayed frozen. The benchmark runner was TabArena revision a98c33817cec8f14b496f5a3194a5138697502a1 with AutoGluon 1.6.4b20261003.

Both outer-test and out-of-fold errors were recomputed from saved predictions. Row IDs and target values were checked against OpenML for 346,195 outer-test rows and 692,339 out-of-fold validation rows.

| Model or configuration | Matched-pool Elo | Rank out of 94 |
|---|---:|---:|
| Kumo Small + CellRidge-448 | 983.9 | 86 |
| Published Kumo Tabular Small (default) | 1838.4 | 5 |

The comparison uses the 93 reference configurations with directly observed results on all 51 first splits in the November 7, 2026 reference snapshot. It includes multiple configurations of some methods. We excluded configurations with missing or imputed entries. We used the TabArena Elo implementation with RF (default) calibrated to 1000, 200 bootstrap rounds, and seed 42. These ranks describe this local comparison. Maintainers independently rerun a contribution before they publish a leaderboard entry.

The candidate beat published Kumo Small on 2 of 51 tasks and lost on 49. The wins were binary classification tasks. Kumo Small's published default uses its own larger context budget and 8 preprocessing members. This comparison changes the pipeline as well as the checkpoint and readout.

**48 of these 51 outer test partitions contributed examples to checkpoint selection.** [Development exposure](DEVELOPMENT.md) lists them. The independent synthetic holdouts used during development are separate from these results.

[Verified split metrics](verified-splits.csv) · [Per-task comparison with Kumo Small](paired-kumo.csv) · [Matched leaderboard](matched-leaderboard.csv) · [Comparison metadata](comparison.json)
