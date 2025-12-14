Xmporph
## Pipeline Stages

1. **Stage 1 – Tumor Segmentation**
   - DeepLabV3-based semantic segmentation to localize tumor regions.

2. **Stage 2 – Tumor-Specific & Information-Weighted Features**
   - Extraction of radiological features and information-weighted boundary time-series.

3. **Stage 3–5 – Deep Features, Feature Fusion, and Classification**
   - CNN-based deep feature extraction (ResNet-50)
   - Feature fusion with tumore specific features 
   

4. **Stage 6 – Dual-Channel Explainability**
   - Visual explainability using Grad-CAM
   - Quantitative and textual interpretation outputs

---

## Repository Structure

```
.
├── Stage1_DeepLabV3_Segmentation.ipynb
├── Stage2_Tumor_Specific_Features.ipynb
├── Stage(3_4_5)_Deep Features_Features Fusion_Classification.ipynb
├── Stage6_Dual-Channel Visual–Textual Explainability.ipynb
├── Brain_Dataset/
│   ├── glioma/
│   ├── meningioma/
│   └── pituitary/
├── outputs/
└── requirements.txt
```

---

## Dataset Format (Expected)

- Data organized by class: `glioma`, `meningioma`, `pituitary`
- Each sample includes:
  - `*_image.png` : CE-T1 MRI image

---

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

---

## Execution Order

Run notebooks sequentially:

1. Stage1_DeepLabV3_Segmentation.ipynb  
2. Stage2_Tumor_Specific_Features.ipynb  
3. Stage(3_4_5)_Deep Features_Features Fusion_Classification.ipynb  
4. Stage6_Dual-Channel Visual–Textual Explainability.ipynb  

> Update dataset and output paths inside each notebook before execution.

---

## Expected Outputs

- **Stage 1**
  - Trained segmentation model checkpoint (`.pth`)
  - Predicted tumor masks 

- **Stage 2**
  - Tumor-specific features
  - Information-weighted time-series arrays (`.npy`)
  - Class label arrays (`.npy`)

- **Stage 3–5**
  - Deep feature embeddings
  - Fused feature representations

- **Stage 6**
  - Trained classifier checkpoint
  - LLM_Prompt_test (`.csv`)
  - Grad-CAM visual explanations (`.png`)

---

## Notes

- Supports local execution and Google Colab.
- For reproducibility, fixed random seeds are recommended.
- This code is intended for research use.
