# XMorph: Explainable Brain Tumor Analysis Via LLM-Assisted Hybrid Deep Intelligence

<p align="center">
  <img src="src/logo.png" width="400" alt="XMorph Logo">
</p>

The official implementation of **XMorph**, a clinically interpretable and computationally efficient framework for fine-grained brain tumor classification. XMorph bridges the gap between high-performance deep learning and clinical trust by fusing deep visual features, nonlinear dynamics (**IWBN**), and quantitative radiological biomarkers with dual-channel explainability.

---

## 📊 Performance Summary
Validated results on the Figshare and BraTS datasets as detailed in the accompanying paper:

| Metric | Result |
| :--- | :--- |
| **Classification Accuracy** | **96.0%** |
| **Segmentation Dice Score (WT)** | **0.932** |
| **Interpretability** | **Dual-Channel** (Visual + Textual) |

---

## 🔍 Capability Comparison
How **XMorph** differs from existing state-of-the-art diagnostic tools:

| Feature / Capability | Standard CNNs [4] | Sultan et al. [13] | Rashed et al. [9] | **XMorph (Ours)** |
| :--- | :---: | :---: | :---: | :---: |
| Deep Feature Learning | ✅ | ✅ | ✅ | **✅** |
| Fractal Dimension (FD) | ❌ | ✅ | ❌ | **✅** |
| Chaotic Metrics (ApEn, LE) | ❌ | ❌ | ❌ | **✅** |
| **IWBN (Boundary Enhancement)** | ❌ | ❌ | ❌ | **✅** |
| **Clinical Biomarker Fusion** | ❌ | ❌ | ❌ | **✅** |
| Visual XAI (Grad-CAM++) | ✅ | ✅ | ❌ | **✅** |
| Textual XAI (LLM Rationales) | ❌ | ❌ | ✅ | **✅** |

---

## ⚙️ Pipeline Stages

1. **Stage 1 – Automated Tumor Segmentation**
   - **Input:** Raw CE-T1 MRI Image.
   - **Process:** DeepLabV3-based semantic segmentation using a ResNet-50 backbone.
   - **Output:** Binary tumor mask and boundary contour.

2. **Stage 2 – Tumor-Specific & IWBN Features**
   - **Input:** Tumor Mask + Boundary Contour.
   - **Process:** Extraction of radiological clinical features (REI, MLS) and our novel **Information-Weighted Boundary Normalization (IWBN)** time-series.
   - **Output:** Quantitative feature arrays (`Non_Linear_Features.npy`, `clinical_features.npy`).

3. **Stage 3–5 – Feature Fusion and Classification**
   - **Input:** Deep CNN Embeddings + Stage 2 Feature Vectors.
   - **Process:** PCA-based dimensionality reduction followed by synergistic fusion and classification via an optimized **XGBoost** model.
   - **Output:** Predicted tumor class (Glioma, Meningioma, Pituitary) and confidence scores.

4. **Stage 6 – Dual-Channel Explainability**
   - **Input:** Model Weights + SHAP values of fused features.
   - **Process:** Generation of visual Grad-CAM++ saliency maps and LLM-assisted diagnostic narratives (GPT-5).
   - **Output:** Interpretable visual heatmaps and textual clinical rationales.
---

## 📝 Notes

Reproducibility: All experiments use fixed random seeds (see notebooks).

LLM Stage: Textual explanations are exported as CSV files and can be re-processed with GPT-4 or GPT-5 for deterministic narrative reproduction.

---

## 📂 Repository Structure

```text
.
├── Script/                              # Sequential execution notebooks
│   ├── Stage1_DeepLabV3_Segmentation.ipynb
│   ├── Stage2_Tumor_Specific_Features.ipynb
│   ├── Stage(3_4_5)_Deep Features_Features Fusion_Classification.ipynb
│   └── Stage6_Dual-Channel Visual–Textual Explainability.ipynb
├── src/                                 # Source data and assets
│   ├── Dataset/                         # CE-T1 MRI samples organized by class
│   ├── figure/                          # Result plots (ROC, Grad-CAM, etc.)
│   ├── Non_Linear_Features.npy          # Extracted handcrafted chaotic metrics
│   ├── clinical_features.npy            # Quantitative radiological biomarkers
│   ├── information_weighted_time_series.npy # IWBN-enhanced boundary signals
│   ├── labels.npy                       # Ground truth class labels
│   ├── llm_prompts_testset.csv          # Structured data for reproducible GPT-5 inference
│   └── logo.png                         # Project branding
├── requirements.txt                     # Python dependencies
└── README.md                            # This file
---



