# Android Mobile Malware Detection Using Machine Learning

This repository contains the code, dataset structure, and reproducible experiment workflow for an undergraduate thesis on Android malware detection using machine learning.

The study evaluates conventional machine-learning classifiers using static Android application features derived from permissions and API-call-related indicators. It is an offline static-analysis baseline evaluation—not a new malware-detection algorithm, an on-device Android application, or a real-time security product.

For the complete run procedure and experiment protocol, see [REPRODUCIBILITY.md](REPRODUCIBILITY.md).

## Project Overview

Android applications may request permissions and use framework APIs that provide access to device information, messaging, network connectivity, services, and other resources. This project uses a Drebin-derived dataset to evaluate whether these static indicators can distinguish benign Android applications from suspicious/malware samples.

The primary evaluation compares four established classifiers:

- Random Forest (RF)
- Support Vector Machine (SVM)
- Decision Tree (DT)
- K-Nearest Neighbours (KNN)

The project also includes:

- Stratified 80:20 train-test splitting
- Five-fold stratified cross-validation on the training set
- StandardScaler pipelines for SVM and KNN
- Accuracy, weighted Precision, weighted Recall, weighted F1-score, and ROC-AUC
- ROC curves and confusion matrices
- Random Forest feature-importance analysis
- PCA explained-variance analysis
- LazyPredict exploratory classifier screening

## Final Experiment

The final experiment uses a processed Drebin-derived static Android malware dataset.

| Item | Configuration |
|---|---|
| Original dataset records | 7,255 |
| Labelled samples used | 7,254 |
| Removed records | 1 row with a missing class label |
| Benign samples | 1,694 |
| Suspicious/malware samples | 5,560 |
| Static features | 215 |
| Train-test split | Stratified 80:20 split |
| Random seed | 42 |
| Training samples | 5,803 |
| Held-out test samples | 1,451 |
| Cross-validation | Five-fold StratifiedKFold with shuffling |
| Scaling | StandardScaler for SVM and KNN |
| PCA analysis | 140 components retain 95% explained variance |
| LazyPredict screening | 20 PCA components retain 47.88% variance |

One feature, `TelephonyManager.getSimCountryIso`, contained five unknown `?` values. These values are converted to `0` before model training so that the feature can be treated numerically.

## Primary Results

| Model | CV Accuracy | Test Accuracy | Weighted Precision | Weighted Recall | Weighted F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Random Forest | 97.42 ± 0.49 | 97.79 | 97.79 | 97.79 | 97.78 | 0.9978 |
| SVM | 96.86 ± 0.64 | 97.52 | 97.63 | 97.52 | 97.55 | 0.9961 |
| Decision Tree | 96.07 ± 0.81 | 96.00 | 95.98 | 96.00 | 95.99 | 0.9399 |
| KNN | 95.31 ± 0.82 | 95.45 | 95.50 | 95.45 | 95.33 | 0.9809 |

Random Forest achieved the strongest held-out baseline performance, with 97.79% test accuracy, 97.78% weighted F1-score, and ROC-AUC of 0.9978. It also produced fewer false negatives than SVM in this evaluation.

These findings apply to the processed Drebin-derived dataset under the documented protocol. They do not demonstrate performance on current Android malware, real-time detection ability, or on-device deployment performance.

## Repository Structure

```text
AcademicThesis/
│
├── data/
│   └── Drebin Dataset.csv
│
├── notebooks/
│   ├── Android Malware Final Code.ipynb
│   ├── Drebin_Malware_Classification_Colab_Ready.ipynb
│   ├── LazyPredict_Drebin.ipynb
│   ├── featureSelection.ipynb
│   └── modelComparison.ipynb
│
├── .gitignore
├── README.md
├── REPRODUCIBILITY.md
└── requirements.txt
```

## Main Notebook

The primary notebook for reproducing the final thesis experiment is:

```text
notebooks/Android Malware Final Code.ipynb
```

This is the authoritative final notebook. It contains the experiment workflow used for the reported baseline results, including:

- Dataset loading and inspection
- Missing-label removal
- Preprocessing of static permission and API-call-related features
- Stratified 80:20 train-test split with random seed 42
- Five-fold cross-validation on the training data
- Random Forest, SVM, Decision Tree, and KNN evaluation
- Classification reports and held-out test metrics
- ROC curves
- Confusion matrices
- Random Forest feature importance
- PCA cumulative explained variance
- Exploratory LazyPredict screening

## Supporting Notebooks

| Notebook | Purpose |
|---|---|
| `Drebin_Malware_Classification_Colab_Ready.ipynb` | Earlier Colab-ready classification and exploratory workflow |
| `LazyPredict_Drebin.ipynb` | Earlier LazyPredict and feature-selection experiments |
| `featureSelection.ipynb` | Exploratory feature-selection work |
| `modelComparison.ipynb` | Additional model-comparison work |

The supporting notebooks are retained for transparency and development history. Their preprocessing, model selection, or outputs may differ from the final experiment. Use `Android Malware Final Code.ipynb` for the final reported results.

## Dataset

The dataset is located at:

```text
data/Drebin Dataset.csv
```

It contains 215 static Android application features, including permissions and API-call-related indicators. The final classification labels are:

- `B`: Benign application
- `S`: Suspicious/malware application

The underlying Drebin benchmark is an older Android malware dataset. Users should verify the source dataset licence and institutional rules before redistributing, reusing, or modifying the CSV file.

## Installation

Use Python 3 and install the required libraries:

```bash
pip install -r requirements.txt
```

The main dependencies are:

```text
numpy
pandas
scikit-learn
matplotlib
seaborn
lazypredict
```

## How to Run

1. Clone or download this repository.
2. Install dependencies using `pip install -r requirements.txt`.
3. Open the primary notebook:
   ```text
   notebooks/Android Malware Final Code.ipynb
   ```
4. Ensure the notebook points to:
   ```text
   data/Drebin Dataset.csv
   ```
5. Run the cells sequentially from top to bottom.
6. Review the generated metrics, tables, ROC curves, confusion matrices, feature-importance plot, PCA plot, and exploratory LazyPredict ranking.

The notebook can be run in Google Colab or Jupyter Notebook. If using Google Colab, upload the dataset or adjust the notebook dataset path as required.

## Interpretation and Limitations

This work is a reproducible baseline experiment based on static features and an older Drebin-derived dataset. The reported scores should not be interpreted as evidence of:

- A newly proposed malware-classification algorithm
- State-of-the-art Android malware detection
- Real-time Android protection
- On-device deployment feasibility
- Low latency, low memory use, or low battery consumption
- Generalisation to current Android malware families
- Detection of dynamic code loading, reflection, encrypted payloads, runtime network behaviour, or sandbox-evasion behaviour

The primary four-model comparison uses fixed, documented configurations. It does not use automated hyperparameter optimisation such as `GridSearchCV` or `RandomizedSearchCV`. PCA and LazyPredict are exploratory analyses only and do not replace the primary comparison.

## Citation

If you use or adapt this repository, please cite the associated thesis/paper and the original Drebin work:

```text
D. Arp, M. Spreitzenbarth, M. Hübner, H. Gascon, and K. Rieck,
“Drebin: Effective and Explainable Detection of Android Malware in Your Pocket,”
Proceedings of the Network and Distributed System Security Symposium (NDSS), 2014.
```

## Licence

This repository is provided for academic and educational purposes. Contact the authors before substantial reuse, redistribution, or commercial use.
