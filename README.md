# Biomass

Predicting pasture biomass components from top-view images for the CSIRO biomass challenge. Given a pasture photo, the model estimates five quantities (grams): `Dry_Green_g`, `Dry_Dead_g`, `Dry_Clover_g`, `GDM_g`, and `Dry_Total_g`.

## Notebooks

- **`EDA.ipynb`** — Exploratory data analysis of the training set: target distributions, species breakdown, per-state statistics, NDVI / plate-height correlations, and image sanity checks.
- **`siglep.ipynb`** — Modeling notebook. Extracts image embeddings with SigLIP / DINOv3 vision backbones, combines them with the tabular features (`Pre_GSHH_NDVI`, `Height_Ave_cm`, `State`, `Species`, `Sampling_Date`), and trains per-target regressors to produce the submission.

## Data

The dataset is not included in this repo. Expected layout under `csiro-biomass/`:

```
csiro-biomass/
├── train.csv
├── test.csv
├── sample_submission.csv
├── train/   # training JPEGs
└── test/    # test JPEGs (hidden at scoring time)
```

See `description.md` for the full schema.

## Approach (siglep.ipynb)

1. Encode each image with a frozen vision backbone (SigLIP, DINOv3) → embedding vector.
2. Concatenate embeddings with tabular/meta features.
3. Fit one regressor per `target_name` and assemble predictions into `submission.csv`.

## Citation

```
@misc{liao2025estimatingpasturebiomasstopview,
  title={Estimating Pasture Biomass from Top-View Images: A Dataset for Precision Agriculture},
  author={Qiyu Liao and Dadong Wang and Rebecca Haling and Jiajun Liu and Xun Li and Martyna Plomecka and Andrew Robson and Matthew Pringle and Rhys Pirie and Megan Walker and Joshua Whelan},
  year={2025},
  eprint={2510.22916},
  archivePrefix={arXiv},
  primaryClass={cs.CV},
  url={https://arxiv.org/abs/2510.22916},
}
```
