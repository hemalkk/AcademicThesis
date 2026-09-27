# Android Mobile Malware Detection Using Machine Learning

This repository contains the implementation code, dataset structure, and reproducible experiment workflow for an undergraduate thesis and conference paper on Android malware detection using machine learning.

The project evaluates conventional machine-learning classifiers using static Android application features derived from permissions and API-call-related indicators. It is presented as a reproducible baseline evaluation, not as a newly proposed malware-classification algorithm or a deployed real-time Android security system.

## Project Scope

The project uses a Drebin-derived Android malware dataset and evaluates static analysis features without executing Android applications.

The primary experiment compares:

- Random Forest (RF)
- Support Vector Machine (SVM)
- Decision Tree (DT)
- K-Nearest Neighbours (KNN)

The workflow also includes:

- Stratified 80:20 train-test splitting
- Five-fold stratified cross-validation
- StandardScaler for SVM and KNN
- Accuracy, weighted Precision, weighted Recall, weighted F1-score, and ROC-AUC evaluation
- Random Forest feature-importance analysis
- PCA exploratory dimensionality-reduction analysis
- LazyPredict exploratory classifier screening

## Final Experiment Summary

The final reproducible experiment used:

| Item | Value |
|---|---|
| Dataset | Drebin-derived static Android dataset |
| Total records | 7,255 |
| Labelled samples used | 7,254 |
| Benign samples | 1,694 |
| Suspicious/malware samples | 5,560 |
| Static features | 215 |
| Train-test split | Stratified 80:20 split |
| Random seed | 42 |
| Training samples | 5,803 |
| Held-out test samples | 1,451 |
| Validation | Five-fold StratifiedKFold cross-validation |
| PCA result | 140 components retain 95% explained variance |
| LazyPredict screening | 20 PCA components retain 47.88% variance |

## Primary Results

| Model | CV Accuracy | Test Accuracy | Weighted F1-score | ROC-AUC |
|---|---:|---:|---:|---:|
| Random Forest | 97.42 ± 0.49 | 97.79 | 97.78 | 0.9978 |
| SVM | 96.86 ± 0.64 | 97.52 | 97.55 | 0.9961 |
| Decision Tree | 96.07 ± 0.81 | 96.00 | 95.99 | 0.9399 |
| KNN | 95.31 ± 0.82 | 95.45 | 95.33 | 0.9809 |

Random Forest achieved the strongest held-out test performance in this baseline evaluation. These results apply to the processed Drebin-derived dataset and should not be interpreted as evidence of real-time Android deployment capability or generalisation to modern malware families.

## Repository Structure

```text
AcademicThesis/
│
├── data/
│   └── Drebin Dataset.csv
│
├── notebooks/
│   ├── Drebin_Malware_Classification_Colab_Ready.ipynb
│   ├── LazyPredict_Drebin.ipynb
│   ├── featureSelection.ipynb
│   └── modelComparison.ipynb
│
└── README.md
```

## Notebooks

### `Drebin_Malware_Classification_Colab_Ready.ipynb`

This notebook contains the main Android malware-classification workflow. It:

- Loads and prepares the Drebin-derived dataset
- Uses static permission and API-call-related features
- Splits data using an 80:20 stratified split
- Trains Random Forest, SVM, Decision Tree, and KNN
- Evaluates Accuracy, Precision, Recall, F1-score, ROC-AUC, ROC curves, and confusion matrices
- Performs Random Forest feature-importance analysis
- Performs PCA explained-variance analysis

### `LazyPredict_Drebin.ipynb`

This notebook performs exploratory classifier screening. It:

- Applies a PCA-reduced representation
- Evaluates multiple individual classifiers using LazyPredict
- Produces a ranked classifier comparison
- Generates a top-classifier accuracy visualisation

LazyPredict results are exploratory only. They do not represent a tuned ensemble model and do not replace the primary four-model evaluation.

### `featureSelection.ipynb`

This notebook contains exploratory feature-selection work.

### `modelComparison.ipynb`

This notebook contains additional model-comparison experiments.

## Dataset

The dataset file is located in:

```text
data/Drebin Dataset.csv
```

The processed dataset contains static Android application features, including permission and API-call-related indicators. The target labels are:

- `B`: Benign
- `S`: Suspicious/malware

The repository is intended for academic and reproducibility purposes only. Users should review the dataset licence and applicable usage conditions before reuse.

## How to Run

1. Clone or download this repository.
2. Open a notebook from the `notebooks/` folder in Google Colab or Jupyter Notebook.
3. Ensure that the dataset path points to:
   ```text
   data/Drebin Dataset.csv
   ```
4. Install the required Python packages if necessary:
   ```python
   !pip install pandas numpy scikit-learn matplotlib seaborn lazypredict
   ```
5. Run notebook cells sequentially.
6. Review the generated evaluation metrics, ROC curves, confusion matrices, feature-importance chart, PCA analysis, and LazyPredict ranking.

## Requirements

The notebooks use the following main Python libraries:

- Python 3
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- lazypredict

## Limitations

This repository supports an offline static-analysis baseline experiment. It does not provide:

- A new malware-classification algorithm
- Real-time Android malware detection
- On-device deployment measurements
- Latency, battery, memory, or model-size evaluation
- Validation using recent or time-separated Android malware datasets
- Dynamic runtime or hybrid behavioural features
- Fully optimised hyperparameter tuning for the primary four-model comparison

## Academic Use and Citation

This repository is intended for academic use. If you use or adapt this work, please cite the associated paper and the original Drebin work:

```text
D. Arp, M. Spreitzenbarth, M. Hübner, H. Gascon, and K. Rieck,
“Drebin: Effective and Explainable Detection of Android Malware in Your Pocket,”
in Proceedings of the Network and Distributed System Security Symposium (NDSS), 2014.
```

## Licence

This repository is provided for academic and educational purposes. Please contact the authors before substantial reuse, redistribution, or commercial use.
