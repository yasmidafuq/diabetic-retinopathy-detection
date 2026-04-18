# diabetic-retinopathy-detection
Cross-Dataset Generalization in Diabetic Retinopathy Detection using Machine Learning and Deep Learning - Final Year Project, University of Bradford
# Cross-Dataset Generalization in Diabetic Retinopathy Detection

[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue)](https://github.com/yasmidafuq/diabetic-retinopathy-detection)
[![License](https://img.shields.io/badge/License-Academic-green)](https://github.com/yasmidafuq/diabetic-retinopathy-detection)

**Final Year Project - BSc (Hons) Computer Science**  
**University of Bradford, 2026**

---

## Author

**Yaasmeen Abdulkareem**  
Student ID: 23028337  
Supervisor: Professor Savas Konur  
School of Computing and Engineering  
University of Bradford

---

## Project Overview

This project investigates cross-dataset generalization challenges in automated diabetic retinopathy detection by systematically comparing classical machine learning and deep learning approaches across multiple independent datasets with different imaging characteristics.

### Research Question

**Can machine learning models trained on one dataset effectively detect diabetic retinopathy when deployed to different clinical settings with different imaging equipment?**

### Key Finding

 **All models (both classical ML and deep learning) exhibited severe performance degradation (35-50% accuracy drops) when tested on datasets with different imaging characteristics, highlighting critical challenges for real-world clinical deployment.**

This finding has significant implications for medical AI deployment - models achieving 95% accuracy in development may drop to 45-55% accuracy when deployed to hospitals with different equipment.

---

## Models Implemented

### Classical Machine Learning
- **Support Vector Machine (SVM)** - RBF kernel, optimized for non-linear boundaries
- **K-Nearest Neighbors (KNN)** - k=5, Euclidean distance metric
- **Random Forest** - 100 decision trees, ensemble voting
- **Logistic Regression** - L2 regularization, LBFGS solver

### Deep Learning
- **Custom Convolutional Neural Network (CNN)** - 4 conv blocks, trained from scratch
- **ResNet50** - Transfer learning from ImageNet, fine-tuned classification head
- **EfficientNetB3** - Transfer learning from ImageNet, compound scaling architecture

---

## Datasets

| Dataset | Images | Role | Characteristics |
|---------|--------|------|-----------------|
| **APTOS 2019** | 3,662 | Training | Indian screening programs, JPEG, variable quality, field cameras |
| **Messidor** | 1,200 | Cross-dataset test | French hospitals, TIFF, high-resolution, Topcon TRC NW6 cameras |
| **Kaggle DR** | 3,662 | Cross-dataset test | Multi-source, JPEG, standardized preprocessing |

**Dataset Selection Rationale:**
- **APTOS** provides sufficient training data with real-world variability
- **Messidor** maximizes distribution difference (different cameras, format, population)
- **Kaggle DR** tests generalization to similar preprocessing but different origins

---

## 🔬 Experimental Results

### Performance Summary

| Model Category | APTOS Validation | Messidor (Different) | Kaggle DR (Similar) | Domain Shift |
|----------------|------------------|----------------------|---------------------|--------------|
| **Classical ML** | 87-95% | 45-55% | 94-97% | **35-50% drop** ⬇️ |
| **Deep Learning** | 80-94% | 44-55% | 80-85% | **35-40% drop** ⬇️ |

### Detailed Results

**Classical Machine Learning:**
- Random Forest: 95.0% → 52.5% → 96.91% (42.5% drop)
- Logistic Regression: 91.25% → 45.5% → 96.78% (45.75% drop)
- KNN: 90.0% → 45.5% → 93.69% (44.5% drop)
- SVM: 87.5% → 45.5% → 94.46% (42.0% drop)

**Deep Learning:**
- Custom CNN: 94.32% → 54.92% (39.4% drop)
- ResNet50: 83.19% → 45.42% → 85.42% (37.77% drop)
- EfficientNetB3: 80.79% → 44.58% → 80.67% (36.21% drop)

---

## Key Contributions

### 1. Systematic Cross-Architecture Comparison
**First study** to systematically compare classical ML and deep learning for diabetic retinopathy detection under identical experimental conditions (same preprocessing, same datasets, same evaluation metrics).

**Finding:** Domain shift affects both classical and deep learning equally - this is a fundamental challenge, not an architecture-specific limitation.

### 2. Dataset Similarity Analysis
**Demonstrated empirically** that dataset similarity matters more than algorithmic sophistication:
- All models (simple Logistic Regression to sophisticated EfficientNetB3) showed identical patterns
- Excellent performance on similar datasets (APTOS ↔ Kaggle DR)
- Poor performance on different datasets (APTOS ↔ Messidor)

### 3. Clinical Deployment Insights
**Highlighted critical gap** between development metrics and deployment reality:
- Single-dataset validation (80-95% accuracy) does not predict cross-hospital performance (44-55% accuracy)
- Implication: Models require extensive local validation before clinical deployment
- Regulatory and safety considerations for medical AI systems

---

## Technologies & Tools

**Programming & Libraries:**
- Python 3.8+
- TensorFlow 2.15.0 / Keras - Deep learning framework
- scikit-learn 1.3.2 - Classical ML algorithms
- NumPy 1.24.3 - Numerical computing
- Pandas 2.0.3 - Data manipulation
- Matplotlib 3.7.2 / Seaborn 0.12.2 - Visualization
- OpenCV 4.8.0 - Image preprocessing

**Development Environment:**
- Google Colaboratory - GPU-accelerated training
- Google Drive - Dataset and model storage
- Jupyter Notebooks - Experiment documentation

---

## Getting Started

### Installation

```bash
# Clone repository
git clone https://github.com/yasmidafuq/diabetic-retinopathy-detection.git
cd diabetic-retinopathy-detection

# Install dependencies
pip install -r requirements.txt
```

### Running Experiments

1. **Open notebooks in Google Colab** for GPU access
2. **Upload datasets** to Google Drive
3. **Run notebooks in this order:**
   - `RetinalDiseaseFYP.ipynb` - Data preprocessing and exploration
   - `ClassicalML_Cross_Dataset_testing.ipynb` - Classical ML models
   - `CNN_Test_Train.ipynb` - Custom CNN
   - `ResNet50_TrainTest.ipynb` - ResNet50 transfer learning
   - `EfficientNetB3.ipynb` - EfficientNetB3 transfer learning
4. **Results** automatically save to Google Drive

### Reproducing Results

All experiments use **fixed random seeds (42)** for reproducibility:
- Data splitting: `random_state=42`
- Model initialization: `random_state=42`
- Training shuffling: `seed=42`

Running the notebooks will produce **identical results** to those reported in the dissertation.

---

## Methodology

### Preprocessing Pipeline
1. **Grayscale Conversion** - Reduce dimensionality while preserving structure
2. **Gaussian Blur** (5×5, σ=1.0) - Noise reduction
3. **CLAHE** (8×8 tiles, clip=2.0) - Local contrast enhancement
4. **Resize** to 224×224 - Standardize dimensions

### Training Strategy
- **Single-source training:** All models train exclusively on APTOS 2019
- **Cross-dataset validation:** Test on Messidor and Kaggle DR (never seen during training)
- **Binary classification:** Healthy vs Unhealthy (any DR stage)
- **80-20 split:** 2,930 training / 732 validation (stratified)

### Evaluation Metrics
- **Accuracy** - Overall correctness
- **Precision** - Positive prediction accuracy
- **Recall** - Disease detection rate (most critical for screening)
- **F1-Score** - Harmonic mean of precision and recall
- **AUC-ROC** - Threshold-independent performance

---

## Analysis & Discussion

### Why Did Messidor Fail?

**Shortcut Learning:** Models learned dataset-specific artifacts rather than disease features:
- Camera fingerprints (different manufacturers produce distinct signatures)
- JPEG compression patterns (Messidor uses TIFF, no compression artifacts)
- Color space characteristics (different sensors produce different RGB distributions)

**Evidence:** Three classical ML models predicted all Messidor images as a single class (0% precision, 0% recall) - clear indication of complete generalization failure.

### Why Did Kaggle DR Succeed?

**Distribution Similarity:** Despite different origins, Kaggle DR shares key characteristics with APTOS:
- Similar preprocessing (resize, normalization)
- JPEG format with comparable compression
- Screening program context (similar quality variability)

**Implication:** Models can generalize when deployment conditions match training conditions, but fail dramatically when conditions differ.

---

## Future Work

### Technical Improvements
- **Domain Adaptation:** Techniques to handle distribution shift (adversarial training, test-time adaptation)
- **Multi-Source Training:** Combine APTOS, Messidor, and Kaggle DR during training
- **Advanced Features:** Vessel segmentation, lesion detection, attention mechanisms
- **Medical-Specific Transfer Learning:** Pre-train on medical images rather than natural images

### Validation & Deployment
- **Additional Datasets:** Validate on DDR, EyePACS, DRIVE, Messidor-2
- **Clinical Trials:** Evaluation with ophthalmologists, inter-rater agreement studies
- **Explainability:** Grad-CAM, SHAP analysis to understand model decisions
- **Real-World Deployment:** Integration with clinical workflows, continuous monitoring

---

## Academic Context

### Legal, Social, Professional, Ethical, Industrial (LSPEI) Considerations

**Legal:** GDPR/HIPAA compliance, medical device regulations, liability for misdiagnosis

**Social:** Healthcare equity (domain shift could widen disparities if models fail in underserved settings)

**Professional:** Responsibility to demand cross-dataset validation before deployment

**Ethical:** Algorithmic bias, transparency requirements, automation bias risks

**Industrial:** Validation costs, scalability challenges, need for standardized protocols

---

## Citation

If you use this work in your research, please cite:

```bibtex
@fypthesis{abdulkareem2026crossdataset,
  author = {Abdulkareem, Yaasmeen},
  title = {Cross-Dataset Generalization in Diabetic Retinopathy Detection using Machine Learning and Deep Learning},
  school = {University of Bradford},
  year = {2026},
  type = {Final Year Project},
  note = {BSc (Hons) Computer Science}
}
```

---

## Acknowledgements

- **Professor Savas Konur** - Project supervision and guidance
- **School of Computing and Engineering, University of Bradford** - Resources and academic support
- **Dataset Creators** - APTOS 2019, Messidor, Kaggle Diabetic Retinopathy datasets
- **Google Colaboratory** - Free GPU access for deep learning training

---

## Contact

**Yaasmeen Abdulkareem**  
University of Bradford  
GitHub: [@yasmidafuq](https://github.com/yasmidafuq)

---

## License

This project is submitted as part of academic coursework at the University of Bradford. All rights reserved.

---

**If you find this project interesting or useful, please consider starring the repository!**

---

*Last updated: April 2026*
