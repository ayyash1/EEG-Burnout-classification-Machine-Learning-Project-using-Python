# 🧠 EEG Burnout Classification

## 🔍 Project Overview

This project aims to develop a machine learning pipeline to classify burnout levels—**Low**, **Medium**, or **High**—based on **raw EEG signal data**. The workflow involves preprocessing EEG recordings, segmenting them into meaningful chunks, extracting statistical features, and training classifiers to accurately predict burnout levels.

---

## 📁 Dataset Description

- **Source**: Raw EEG data (~3GB) collected from **30 patients**.
- **Conditions**: Eyes Open & Eyes Closed.
- **Format**:
  - Each patient has multiple `.csv` files (up to 3 per condition).
  - Each file contains ~3 minutes of EEG data (~50,000 rows).
- **Labels**: Each EEG file is labeled using **Maslach Burnout Inventory (MBI)** scores.

---

## 🧹 Data Preprocessing

### ✅ Cleaning
- Removed null and duplicate values.
- Verified timestamp and signal consistency.

### ✅ Labelling
- Each EEG file is associated with a burnout level from the subject’s MBI score.

### ✅ Segmentation
- **Method**: Sliding window.
- **Window Size**: 10 seconds (to avoid data loss from sample-count-based segmentation).
- **Outcome**: ~18 segments per 3-minute file.

---

## 🧠 Feature Extraction

From each 10-second EEG segment, features are extracted from four primary channels:
- `RAW_AF7`, `RAW_AF8`, `RAW_TP9`, `RAW_TP10`

### Extracted Features:
- **Statistical**: Mean, Std Deviation, Skewness, Kurtosis
- **Signal-based**: Zero Crossing Rate, Line Length
- **Hjorth Parameters**: Activity, Mobility, Complexity
- **Demographic**: Encoded Gender

> 💡 A total of **36 features** are generated per segment.

---

## 🤖 Model Training & Evaluation

### 1️⃣ Logistic Regression (L2 Regularized)
- **Accuracy**: 70%
- **Cross-Validation (5-fold)**: 69.43%
- **Precision (macro)**: 93%
- **F1-score (macro)**: 92%
- **Recall (macro)**: 92%

> ⚠️ Good metrics but poor generalization—overfit on small data (~1GB), degraded on full dataset (~3GB).

---

### 2️⃣ Random Forest Classifier (Final Model)
- **Accuracy**: 92.4%
- **Cross-Validation (5-fold)**: 92.26%
- **Precision (macro)**: 93%
- **F1-score (macro)**: 92%
- **Recall (macro)**: 92%

> ✅ Superior generalization, robust to non-linear patterns, performs consistently across datasets.

---

## 🧩 Challenges & Solutions

| Challenge                             | Solution                                                                 |
|--------------------------------------|--------------------------------------------------------------------------|
| Data loss due to fixed-size segments | Switched to **time-based (10s)** sliding window segmentation             |
| Poor generalization in simple models | Adopted **Random Forest** for handling complex EEG variations            |
| Large data volume (3GB)              | Applied memory-efficient processing and optimized loops                  |
| Label inconsistencies                | Ensured each file is labeled using subject's unique MBI-derived burnout |

---

## 🚀 Deployment

The final model is integrated into a **Streamlit-based GUI**, allowing:

- Upload of raw EEG `.csv` files.
- Automated processing & feature extraction.
- **Burnout level prediction**.
- Personalized advisory message based on predicted state.

> 🎯 Designed for non-technical users like **clinicians** or **researchers** for easy mental health assessment using EEG data.

---

## ✅ Conclusion

This project demonstrates how **feature-based machine learning** can effectively classify **burnout levels** using EEG signals. With systematic preprocessing, robust feature extraction, and model evaluation, this approach shows promise for real-world mental health diagnostics.

---

## 🛠️ Technologies Used

- Python
- Pandas, NumPy
- Scikit-learn
- Streamlit
- SciPy
- EEG signal processing techniques

---

## 📌 Future Work

- ✅ GUI Deployment (Completed)
- ⏳ Model Fine-tuning with additional datasets
- ⏳ Integration with wearable EEG devices

---

## 📬 Contact

For questions or collaborations, feel free to reach out
