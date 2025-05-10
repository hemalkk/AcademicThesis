# Android Mobile Malware Detection Using Machine Learning

This repository contains the implementation code and results for our undergraduate thesis and conference paper on Android malware detection using machine learning. The project uses the Drebin dataset and focuses on lightweight static analysis techniques suitable for mobile devices.

## 📘 Project Focus

Our approach performs static analysis of Android apps based on permissions and API calls. We train and evaluate multiple machine learning models for classifying malware and benign apps.

Two main notebooks are included:

### 🧪 `Drebin_Malware_Classification_Colab_Ready.ipynb`
- Loads and preprocesses the Drebin dataset
- Applies PCA for dimensionality reduction
- Trains ML models (Random Forest, SVM, DT, KNN)
- Evaluates accuracy, F1-score, ROC-AUC, and confusion matrix

### ⚙️ `LazyPredict_Drebin.ipynb`
- Benchmarks 30+ ML classifiers using LazyPredict
- Automatically identifies high-performing models
- Confirms the robustness of selected classifiers (e.g., RF, SVM)
- Visualizes top model accuracies

## 📂 Dataset

- `Drebin Dataset.csv` — extracted static features (permissions, API calls) from Android apps

## 👥 Group Project

This is a group research project under the Department of Computer Science, American International University-Bangladesh (AIUB), guided by faculty supervisors.  
The implementation supports our accepted conference paper submitted in April 2025.

## 🚀 How to Use

1. Open the two main notebooks in **Google Colab** or Jupyter.
2. Run all cells sequentially to:
   - Train models
   - Analyze performance
   - View ROC curves and classification reports

## 📌 Note

No figures are included in the repo — all plots are dynamically generated when running the notebooks.

## 📄 License

This project is for academic use only. Please cite this repository or contact the authors before reuse.

