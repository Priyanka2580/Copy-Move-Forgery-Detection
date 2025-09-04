# Robust Copy-Move Forgery Detection in Images using DCT and HOG Feature Fusion

## 📌 Project Overview
In today’s digital world, image authenticity is increasingly threatened by advanced tampering techniques. One of the most common manipulations is **Copy-Move Forgery (CMF)**, where parts of an image are copied and pasted within the same or another image. Such forgeries are often seamless and challenging to detect by the human eye, posing risks in journalism, forensics, and cybersecurity.

This project presents a **block-based hybrid approach** for detecting copy-move forgery using **Discrete Cosine Transform (DCT)** and **Histogram of Oriented Gradients (HOG)** feature fusion, combined with **feature vector shuffling** to improve robustness. The proposed method enhances detection accuracy under various post-processing operations like compression, noise addition, blurring, and contrast/brightness changes.

---

## ⚙️ Methodology
The proposed **CMFD workflow** includes:

1. **Preprocessing**  
   - Convert input image (RGB) to grayscale.  

2. **Overlapping Block Division**  
   - Divide grayscale image into overlapping blocks of varying sizes. We have tested with block-size=3,5,7.  

3. **Feature Extraction**  
   - Extract **DCT coefficients** (frequency features).  
   - Extract **HOG descriptors** (structural/gradient features).  
   - Fuse both into a combined feature vector.  

4. **Feature Vector Shuffling**  
   - Shuffle feature components to improve robustness against post-processing.  

5. **Feature Matching**  
   - Sort feature vectors lexicographically.  
   - Identify candidate matches using similarity thresholds and spatial distance.  

6. **False Match Elimination**  
   - Use **shift vector analysis** to retain only consistent duplicates.  

7. **Postprocessing**  
   - Generate binary prediction map.  
   - Apply morphological operations (dilation, erosion) to refine forged regions.  

---

## 🗂 Dataset
- **CoMoFoD Dataset** (Copy-Move Forgery Detection Dataset)  
- 10,400 images across 200 sets, each containing:  
  - 25 forged images, 25 original images  
  - Ground truth masks  
- Image resolution: 512 × 512 pixels  
- Includes transformations: translation, rotation, scaling, distortion, and combined manipulations
- Our study focuses on 40 small-sized images set each of 52 patterns, i.e. 2080 images, specifically translation-based forgeries with post-processing variations.

---

## 📊 Evaluation Metrics
- **Precision (Pr)**  
- **Recall (Re)**  
- **F1-score**  
- **True Negative Rate (TNR)**  
- **Balanced Accuracy**  
- **Overall Accuracy**

These are computed on **pixel-level classification** of forged vs. non-forged regions.

---

## 🚀 Results
- **Using DCT only:**  
  - Precision up to **82.57%**, Recall **93.16%**  
- **Using HOG only:**  
  - Precision improved with larger block size (up to **81.48%**)  
- **DCT + HOG fusion (no shuffle):**  
  - Precision **83.29%**, Recall **93.16%**  
- **DCT + HOG with shuffle (best results):**  
  - Precision **83.47%**, Recall **93.13%**, Accuracy **99.24%**

### Performance against post-processing:
- **Brightness/Contrast changes:** Stable performance with F1 ~ 87%  
- **Color reduction:** Slight performance drop (F1 ~ 86%)  
- **Blurring:** Moderate blur improves detection, heavy blur reduces recall  
- **JPEG compression & noise:** Significant performance decline (vulnerability area)  

### Comparison with state-of-the-art:
- Outperforms traditional **DCT-only** and some **hybrid methods (DCT+DWT+EOA, HOG+MBF)**  
- Achieves **higher accuracy (99.26%)** than several benchmark methods  

---

## 🔍 Error Analysis
- Struggles with:
  - Heavy JPEG compression and strong additive noise  
  - Small or irregularly shaped forged regions  
  - High-texture similarity regions (false positives)  

---

## ✅ Conclusion
This research demonstrates that **fusing DCT and HOG features with shuffling** significantly improves the robustness and accuracy of copy-move forgery detection. The method performs well under most post-processing conditions and provides competitive results against state-of-the-art methods.

### 📌 Future Work
- Extend detection for **rotation, scaling, and complex distortions**  
- Enhance resilience against **JPEG compression and noise**  
- Validate on additional **benchmark datasets**  

