# Kumo Small + CellRidge, checkpoint 448

This release contains separate classification and regression inference weights for a derivative of NVIDIA Kumo Tabular Small. Four additional row blocks transform the intermediate cell and ICL representations. An affine ridge fit on labeled support rows produces the prediction for each task. The classification readout uses a softmax temperature of 0.25. The native single-member preprocessing recipe uses seed 104.

The [v1.0 release](https://github.com/1587causalai/kumo-small-cellridge-448/releases/tag/v1.0) contains both safetensors files. [weights.json](weights.json) records their SHA-256 digests, byte sizes, and source checkpoint digests. Both exports were verified tensor by tensor against the source. Use the classification file for binary or multiclass tasks and the regression file for numerical targets. Both the backbone and additional blocks were fine-tuned. The release contains the inference tensors only.

## Development and benchmark exposure

The continuation used independent synthetic training tables, 2,048 labeled support rows and 64 query rows per table. Every 16 tables contributed one optimizer update, with a backbone learning rate of 3e-6 and a tail learning rate of 3e-5. Checkpoint 448 is the output of 28 continuation updates.

**Checkpoint selection used labeled outer-test examples from 48 of the 51 TabArena datasets.** We repeatedly scored checkpoints on up to 512 query rows drawn from the first official outer split, amounting to 22,807 labeled query examples. The 448 checkpoint was selected using those scores. Gradient updates in this continuation used synthetic data. The corresponding TabArena-Lite tasks overlap the development panel, so their results measure performance on a benchmark used in development. We cannot claim an independent test on those 48 tasks. [Dataset list](DEVELOPMENT.md)

The local development score was 999.0 Elo under a restricted support/query protocol and a 46-method reference pool. The official TabArena leaderboard uses its own training, validation, test and ranking procedures. Scores and ranking positions from those protocols must be reported separately.

## Source and license

The base weights come from NVIDIA Kumo Tabular, revision 3c3e10bbdb590ace29e7026847f92db3c603096d. The structured-data-models implementation used by this derivative is revision b780fc92b2cd50df5525575f0ddd1ae9038102bc. The weight license is OpenMDW-1.1. [NVIDIA model](https://huggingface.co/nvidia/Kumo-Tabular) · [Pinned implementation](https://github.com/NVIDIA/structured-data-models/tree/b780fc92b2cd50df5525575f0ddd1ae9038102bc) · [License and copyright notice](LICENSE)
