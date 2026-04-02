# Malware Detection from API Call Sequences

Home assignment for the Introduction to Machine Learning course @ PoliTO.

## Task

Binary classification of Windows executables (malware vs. benign) based on sequences of system API calls recorded during dynamic analysis in a sandbox environment.

## Dataset

| Split | Benign | Malware | Total |
|-------|--------|---------|-------|
| Train | 611    | 15,714  | 16,325 |
| Test  | 243    | 6,262   | 6,505  |

The dataset is highly imbalanced (~96% malware). The test set contains API calls not seen during training (OOV).

## Models

| Model | Description |
|-------|-------------|
| **BoW + Random Forest** | API call counts as features; class-weighted RF with grid-search CV |
| **EmbedderMLP** | Learned token embeddings + mean-pooling + MLP classifier |
| **LSTM** | Learned token embeddings + LSTM to preserve call order |

## Results (Test Set)

| Model | Benign F1 | Malware F1 | Macro F1 |
|-------|-----------|------------|----------|
| BoW + RF | 0.63 | 0.99 | **0.81** |
| EmbedderMLP | 0.28 | 0.92 | 0.60 |
| LSTM | 0.59 | 0.98 | 0.78 |

The BoW baseline outperforms both neural models. For this task, the presence of specific API calls is more discriminative than their order.
