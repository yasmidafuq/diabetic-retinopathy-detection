# Cross-Dataset Generalization in Diabetic Retinopathy Detection

**Final Year Project - BSc (Hons) Computer Science**  
University of Bradford, 2026

**Author:** Yaasmeen Abdulkareem (Student ID: 23028337)  
**Supervisor:** Professor Savas Konur

---

## Overview

This project investigates whether machine learning models trained on one dataset can detect diabetic retinopathy when deployed to different clinical settings with different imaging equipment.

**Key Finding:** All models (classical ML and deep learning) exhibited severe performance degradation (35-50% accuracy drops) when tested on datasets with different imaging characteristics, demonstrating critical challenges for real-world clinical deployment.

---

## Models Tested

**Classical Machine Learning:**
- Support Vector Machine (SVM)
- K-Nearest Neighbors (KNN)
- Random Forest
- Logistic Regression

**Deep Learning:**
- Custom CNN (trained from scratch)
- ResNet50 (transfer learning)
- EfficientNetB3 (transfer learning)

---

## Datasets

| Dataset | Images | Role | Source |
|---------|--------|------|--------|
| APTOS 2019 | 3,662 | Training | Indian screening programs |
| Messidor | 1,200 | Test (different) | French hospitals |
| Kaggle DR | 3,662 | Test (similar) | Multi-source |

---

## Results Summary

| Model Type | APTOS | Messidor | Kaggle DR | Drop |
|------------|-------|----------|-----------|------|
| Classical ML | 87-95% | 45-55% | 94-97% | 35-50% |
| Deep Learning | 80-94% | 44-55% | 80-85% | 35-40% |

**Main Finding:** Domain shift affects all approaches equally. Dataset similarity matters more than algorithmic sophistication.
---

## Setup

**Install dependencies:**
```bash
pip install -r requirements.txt
```

**Download datasets:**
- APTOS 2019: https://www.kaggle.com/competitions/aptos2019-blindness-detection
- Messidor: http://www.adcis.net/en/third-party/messidor/
- Kaggle DR: https://www.kaggle.com/c/diabetic-retinopathy-detection

**Run notebooks:**
Open in Google Colab for GPU access, upload datasets to Google Drive, run notebooks sequentially.

---

## Key Contributions

1. First systematic comparison of classical ML vs deep learning under identical conditions
2. Demonstrated that domain shift is universal across all algorithm types
3. Highlighted gap between single-dataset validation and real-world deployment performance

---

## Technologies

Python 3.8+, TensorFlow 2.15.0, scikit-learn 1.3.2, NumPy, Pandas, Matplotlib, OpenCV

---

## Citation
Abdulkareem, Y. (2026). Cross-Dataset Generalization in Diabetic Retinopathy Detection.
Final Year Project, BSc Computer Science, University of Bradford.
---

## Acknowledgements

Professor Savas Konur (supervisor), School of Computing and Engineering at University of Bradford, dataset creators (APTOS, Messidor, Kaggle DR), Google Colaboratory.

---

**Contact:** GitHub @yasmidafuq







