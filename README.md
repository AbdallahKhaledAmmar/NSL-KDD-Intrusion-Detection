# Network Intrusion Detection on NSL-KDD

Machine-learning intrusion detection system (IDS): classifies network connections as **normal** or **attack**, and identifies the attack category (**DoS, Probe, R2L, U2R**).

## Dataset
[NSL-KDD](https://www.unb.ca/cic/datasets/nsl.html) (University of New Brunswick, improved version of KDD'99; Tavallaee et al., 2009). 41 features per connection. Files in `data/`: `KDDTrain+`, `KDDTest+`, `KDDTest-21`.

## Notebooks
| Notebook | What it does |
|---|---|
| `attack-detection.ipynb` | EDA and 20+ visualisations, feature selection, binary classification (Linear SVM, Quadratic SVM, KNN, LSTM) and multi-class classification (KNN, MLP). Evaluated on a 75/25 split of `KDDTrain+`. |
| `evaluation-on-official-test-set.ipynb` | Realistic evaluation: train on `KDDTrain+`, test on the separate `KDDTest+`. |

## Results
| Evaluation | Best accuracy |
|---|---|
| Random 75/25 split of `KDDTrain+` (KNN, binary) | ~99.6% |
| Official `KDDTest+` (KNN, binary) | ~77% (attack recall 0.65) |

The gap is expected: `KDDTest+` contains 17 attack types that never appear in training, so a random split of the training file overstates real-world performance. U2R is also very rare (15 samples in the split test set) and is detected poorly.

## Run
```bash
pip install -r requirements.txt
jupyter notebook
```

## Possible improvements
Handle class imbalance (U2R/R2L), tune hyper-parameters, add anomaly-detection models for unseen attacks, deploy as a small API with Docker.
