# 🧠 Intracranial Hemorrhage (ICH) Detection Pipeline

## 📖 Project Overview
Intracranial hemorrhages (brain bleeds) are life-threatening medical emergencies where every second counts. Rapid and accurate diagnosis from CT scans is crucial for patient survival. 

This project develops an advanced Artificial Intelligence pipeline to assist radiologists. The AI acts as a highly sensitive safety net—automatically detecting if a brain bleed is present and classifying it into one of 5 specific subtypes (*Epidural, Intraparenchymal, Intraventricular, Subarachnoid, or Subdural*).

## 🏆 Our Results: Prioritizing Patient Safety
In medical diagnosis, missing a hemorrhage (a False Negative) is incredibly dangerous. Therefore, we optimized our entire system for **Recall** (Sensitivity) to ensure we cast the widest safety net possible.

- **Task 1 (Bleed Detection):** Achieved an exceptional **96.0% Recall**. This means the AI successfully catches 96 out of every 100 actual brain bleeds, drastically reducing the chance of a missed diagnosis.
- **Task 2 (Subtype Classification):** The model achieved a **Macro Average Recall of 80.3%** across all classes:
  - **Intraparenchymal:** 84.5%
  - **Intraventricular:** 82.9%
  - **Subdural:** 80.3%
  - **Epidural:** 75.3%
  - **Subarachnoid:** 70.6%

## 🔬 Key Innovations & Research

### 1. Hyper-Realistic Synthetic Data (CycleGAN)
In medical datasets, specific types of bleeds are rare. To solve this, we used **CycleGAN** to generate synthetic CT scans. To prove how good our generative AI is, we tested it against a trained model to see if it could tell the difference between real and fake scans. 

Our CycleGAN successfully created images so highly realistic that **97.34%** of them were classified as real clinical CT scans, drastically outperforming traditional data-balancing methods like SMOTE:

<img width="515" height="382" alt="Screenshot 2026-03-11 at 11 01 54 AM" src="https://github.com/user-attachments/assets/51bc12cb-5883-4f9c-8afb-775fe6c865bf" />

### 2. Kernel-Size Ablation Study ($7 \times 7$ Dominance)
We customized a state-of-the-art vision model called `ConvNeXt`. Medical imaging requires specific "vision field" sizes to spot tiny, irregular blood pools. Through a massive ablation study, we tested every kernel size from $3 \times 3$ up to $9 \times 9$. 

The results proved that a **$7 \times 7$ kernel** was the absolute optimal configuration, maximizing Recall without sacrificing Precision:

<img width="1019" height="535" alt="Screenshot 2026-03-11 at 11 01 02 AM" src="https://github.com/user-attachments/assets/9302ac73-7004-40dd-8c5f-a2c30dc14a4d" />


### 3. Medical Image Preprocessing (Windowing & Outlier Removal)
Medical datasets often contain corrupted or anomalous scans that confuse AI models. We implemented a rigorous **Outlier Removal** process to clean the dataset, which drastically improved the model's overall accuracy and learning stability. Furthermore, we applied a clinical technique called **Windowing** to selectively adjust the contrast—specifically highlighting blood, brain tissue, and bone so the hemorrhages become clearly visible.

### 4. Explainable AI (XAI) for Clinical Trust
We integrated visual tools like **Grad-CAM++, LIME, and SHAP** to draw heatmaps directly onto the brain scans. These heatmaps show exactly which pixels the AI looked at to make its diagnosis, proving that it is detecting real medical anomalies.

## 📁 Project Files Layout
* **Data Pipeline:** `01_preprocessing.ipynb` ➔ `02_outlier_removal.ipynb` ➔ `03_data_augmentation.ipynb`
* **Modeling & Training:** `04_model_architecture.ipynb` ➔ `05_training_binary.ipynb` ➔ `06_training_multiclass.ipynb`
* **Results & Analysis:** `07_evaluation.ipynb` ➔ `08_xai_visualizations.ipynb` ➔ `09_ablation_kernel_study.ipynb`

