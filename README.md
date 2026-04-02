# Seizure Classification

This project builds seizure-type classification models from EEG-derived features.

## Dataset Used by the Training Code

The preprocessing function loads this file:

- `Dataset/MASTER_DATASET1.csv`

In the code, this is called with:

- `pd.read_csv("Dataset\\MASTER_DATASET1.csv")`

## IMF5 Dataset (Also Available)

In addition to `MASTER_DATASET1.csv`, this project also includes an IMF5-processed EEG dataset at:

- `Dataset/EEG-VMD-IMF5/`

Folder-level summary:

- Subject folders: 17 (`SUB1` to `SUB17`)
- Total files in IMF5 tree: 34

This dataset is organized by subject and can be used for:

- Subject-wise experimentation
- Per-recording feature extraction
- Comparative experiments against the flattened `MASTER_DATASET1.csv` pipeline

## Dataset Summary

- Total rows (samples): 180
- Total columns: 321
- Feature columns: 320 (named `1` to `320`)
- Label column: `Target`
- Number of classes: 6
- Class distribution:
  - Class 0: 30
  - Class 1: 30
  - Class 2: 30
  - Class 3: 30
  - Class 4: 30
  - Class 5: 30

This is a balanced multi-class dataset.

## Expected Data Format

The training pipeline expects:

- One row per sample
- Numeric feature columns
- Integer class labels in `Target`

Example schema:

- Features: `1, 2, 3, ..., 320`
- Label: `Target`

## Preprocessing Steps in Code

The function `fix_data_preprocessing()` performs:

1. Mean imputation for missing values (`SimpleImputer(strategy='mean')`)
2. Removal of near-zero variance features (`VarianceThreshold`)
3. Removal of highly correlated features (absolute correlation greater than 0.95)
4. Univariate feature selection (`SelectKBest(f_classif, k=min(80, n_features))`)
5. Standard scaling (`StandardScaler`)

The function returns:

- `X_scaled`: processed feature matrix
- `y`: class labels from `Target`

## Project Structure (Relevant)

- `seizureClassification (1).ipynb`: main notebook with preprocessing, model training, and evaluation
- `Dataset/MASTER_DATASET1.csv`: main dataset used by code
- `Dataset/MASTER_DATASET - Copy.csv`: alternate dataset copy
- `Dataset/EEG-VMD-IMF5/`: IMF5-processed EEG files organized by subject

## Run Notes

- Ensure `Dataset/MASTER_DATASET1.csv` exists at the relative path shown above.
- IMF5 data is available under `Dataset/EEG-VMD-IMF5/` if you want to build a subject-wise or file-wise pipeline.
- If you convert the notebook into a script (for example, `seizureClassification.py`), keep the same dataset path or update it consistently.
