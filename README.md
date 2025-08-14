# YOLOv8 Adversarial Patch 

Implementation and evaluation of **adversarial patch attacks** on YOLOv8 object detection in a simulated driving environment, featuring an **Expectation Over Transformation (EOT)** patch generation pipeline and a **Local Gradient Smoothing (LGS)** defense.

This project explores how **physical adversarial patches** can disrupt object detection systems in autonomous driving scenarios, and investigates defenses to improve robustness.

---

##  Dataset

- **Source:** [CARLA-GEAR](https://arxiv.org/abs/2301.01680) — *CARLA-GEAR: A Dataset Generator for a Systematic Evaluation of Adversarial Robustness of Deep Learning Vision Models* (Yaman *et al.*, 2023).  
- **Format Conversion:** Original annotations were provided in **COCO JSON** format. We converted them into **YOLO format** for compatibility with Ultralytics YOLOv8 using a custom conversion script.  
- **Scenarios Used:** Adversarial billboard scenes (`billboard01`–`billboard09`) and clean (no billboard) driving scenes.

---

##  Adversarial Patch Generation

The patch generation follows the **Expectation Over Transformation (EOT)** framework, ensuring robustness under:

- **Spatial transformations:** scaling, rotations, translations  
- **Projective transformations:** perspective changes for realism  
- **Appearance transformations:** brightness, contrast, noise  

### **Pipeline Steps**
1. **Input Images** — From CARLA-GEAR  
2. **Patch Initialization** — Random or pretrained start  
3. **EOT Transformations** — Spatial, projective, and appearance changes  
4. **Patch Application** — Overlay on billboards  
5. **Detection & Loss** — YOLOv8 detects objects in patched images  
6. **Optimization** — Backpropagation updates the patch to maximize detection degradation  

---

##  Local Gradient Smoothing (LGS) Defense

After generating the optimal adversarial patch, we applied **Local Gradient Smoothing (LGS)** — a preprocessing defense that reduces the impact of high-frequency adversarial noise while preserving image content.

- **Goal:** Reduce patch-induced false positives/negatives  
- **Trade-off:** Improves robustness but may slightly reduce clean accuracy  
- **Evaluation:** Compared detection results before and after applying LGS  

---

##  Results

- **Without defense:** Significant accuracy drop due to patch-induced false detections  
- **With LGS defense:** Improved detection performance on attacked images, showing a balance between accuracy and robustness  

---

##  Tools & Libraries

- **[Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics)** – Object detection  
- **PyTorch** – Model training & optimization  
- **OpenCV** – Image processing  
- **Matplotlib** – Visualization  
- **NumPy** – Data manipulation  

---

##  Citation

**Dataset:**
```bibtex
@inproceedings{yaman2023carla,
  title={CARLA-GEAR: A Dataset Generator for a Systematic Evaluation of Adversarial Robustness of Deep Learning Vision Models},
  author={Yaman, Cemal and Humeniuk, Ivan and Pek, Christian and Dietmayer, Klaus},
  booktitle={2023 IEEE Intelligent Vehicles Symposium (IV)},
  year={2023},
  organization={IEEE}
}

