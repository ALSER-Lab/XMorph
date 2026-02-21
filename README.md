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

| Feature / Capability | Deepak & Ameer [4] | Cheng [21] | Mahesh et al. [7] | Saeed et al. [8] | Sultan et al. [13] | Temtam et al. [14] | Rashed et al. [9] | **XMorph (Ours)** |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Deep Feature Learning | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | **✅** |
| Fractal Dimension (FD) | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | ❌ | **✅** |
| Chaotic Metrics (ApEn, LE) | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | **✅** |
| **IWBN (Boundary Enhancement)** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | **✅** |
| **Clinical Biomarkers (REI, MLS, Dskull)** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | **✅** |
| Visual XAI (Heatmaps) | ❌ | ❌ | ✅ | ✅ | ✅ | ❌ | ❌ | **✅** |
| Textual XAI (LLM Rationales) | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | **✅** |

<br>
<small>
<b>References:</b><br>
<b>[4]</b> S. Deepak and P. Ameer, <i>"Brain tumor classification using deep cnn features via transfer learning,"</i> Computers in Biology and Medicine, vol. 111, p. 103345, 2019.<br>
<b>[7]</b> T. R. Mahesh et al., <i>"An xai-enhanced efficientnetb0 framework for precision brain tumor detection in mri imaging,"</i> Journal of Neuroscience Methods, vol. 410, p. 110227, 2024.<br>
<b>[8]</b> T. Saeed et al., <i>"Neuro-xai: Explainable deep learning framework based on deeplabv3+ and bayesian optimization for segmentation and classification of brain tumor in mri scans,"</i> Journal of Neuroscience Methods, vol. 410, p. 110247, 2024.<br>
<b>[9]</b> E. A. Rashed et al., <i>"Automatic generation of brain tumor diagnostic reports from multimodality mri using large language models,"</i> 2025 IEEE 22nd International Symposium on Biomedical Imaging (ISBI), 2025.<br>
<b>[13]</b> H. Sultan et al., <i>"Estimation of fractal dimension and segmentation of brain tumor with parallel features aggregation network,"</i> Fractal and Fractional, vol. 8, no. 6, p. 357, 2024.<br>
<b>[14]</b> A. Temtam, L. Pei, and K. Iftekharuddin, <i>"Computational modeling of deep multiresolution-fractal texture and its application to abnormal brain tissue segmentation,"</i> arXiv preprint arXiv:2306.04754, 2023.<br>
<b>[21]</b> J. Cheng, <i>"Brain tumor dataset,"</i> 2017. [Online]. Available: https://doi.org/10.6084/m9.figshare.1512427.v8
</small>

---

## ⚙️ Pipeline Stages

1. **Stage 1 – Automated Tumor Segmentation**
   - **Input:** Raw CE-T1 MRI Image.
   - **Process:** DeepLabV3-based semantic segmentation using a ResNet-50 backbone.
   - **Output:** Binary tumor mask and boundary contour.

2. **Stage 2 – Tumor-Specific & IWBN Features**
   - **Input:** Tumor Mask + Boundary Contour.
   - **Process:** Extraction of radiological clinical features (REI, MLS) and our novel **Information-Weighted Boundary Normalization (IWBN)** time-series and Non-linear features.
   - **Output:** Quantitative feature arrays (`Non_Linear_Features.npy`, `information_weighted_time_series.npy`,`clinical_features.npy`).

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

Reproducibility: All experiments use fixed random seeds (See Scripts).

LLM Stage: Textual explanations are exported as CSV files and can be re-processed with GPT-4 or GPT-5 for deterministic narrative reproduction.
🚀 Setup & Reproducibility
Notebooks must be run sequentially to maintain the data dependency chain. Follow these steps to set up your environment:
code
Bash
# Create and activate virtual environment
python -m venv .venv
source .venv/bin/activate

# Install dependencies
jupyter notebook
- **Execution Order:**
Script/Stage1_DeepLabV3_Segmentation.ipynb
Script/Stage2_Tumor_Specific_Features.ipynb
Script/Stage(3_4_5)_Deep Features_Features Fusion_Classification.ipynb
Script/Stage6_Dual-Channel Visual–Textual Explainability.ipynb
# 📜 Citation
If you use XMorph in your research, please cite our work
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
│   ├── labels.npy                       # Ground truth class labels
│   ├── llm_prompts_testset.csv          # Structured data for reproducible GPT-5 inference
│   └── logo.png                         # Project branding
├── requirements.txt                     # Python dependencies
└── README.md                            # This file
---



