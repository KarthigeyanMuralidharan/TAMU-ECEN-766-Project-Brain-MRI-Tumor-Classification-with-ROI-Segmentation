# 🧠 Brain MRI Tumor Classification with ROI Segmentation

## 📌 Problem Description

Brain tumors are abnormal growths in brain tissue that can be life-threatening if not detected early. Magnetic Resonance Imaging (MRI) is widely used for brain analysis due to its ability to provide detailed anatomical information. However, manual interpretation of MRI scans can be time-consuming and may vary across radiologists.

The goal of this project is to develop an automated system that can classify brain MRI images into tumor and non-tumor categories using image processing and machine learning techniques.

A key challenge in MRI-based classification is that images contain large regions of non-tumor information such as healthy tissue, skull structures, and background variations. When features are extracted from the entire image, these irrelevant regions can reduce classification accuracy.

To address this issue, this project investigates the impact of introducing a **Region-of-Interest (ROI) segmentation step** before feature extraction. Two approaches are considered:

- **Baseline approach**: Feature extraction from the entire MRI image  
- **Proposed approach**: ROI segmentation followed by feature extraction only from the tumor region  

The objective is to evaluate whether isolating tumor regions improves classification performance.

---

## 📂 Data Description

The system uses publicly available brain MRI datasets containing labeled images. Each MRI slice is treated as an independent sample with an associated class label.

Key characteristics of the dataset:

- Image type: Brain MRI scans  
- Format: 2D grayscale images (converted if necessary)  
- Classes: Binary classification (tumor vs non-tumor)  
- Source: Public datasets and online repositories  

Before processing, all images undergo standardization to ensure consistency:

- Resizing to a fixed spatial resolution  
- Conversion to grayscale (if required)  
- Noise reduction using median filtering  
- Intensity normalization to handle contrast variations  

These preprocessing steps are necessary to reduce variability across images and improve the reliability of subsequent feature extraction and classification stages.

---

## ⚙️ Algorithms and Methods

The system follows a structured pipeline consisting of preprocessing, segmentation, feature extraction, and classification.

---

### 1. Preprocessing

Preprocessing prepares MRI images for analysis by improving image quality and consistency.

- **Median Filtering**: Removes noise while preserving edges  
- **Intensity Normalization**: Reduces brightness and contrast variations  
- **Resizing**: Ensures uniform input dimensions  

---

### 2. ROI Segmentation (Proposed Method)

The ROI segmentation step aims to isolate the tumor region from the rest of the image.

The following techniques are used:

- **Otsu Thresholding**: Automatically determines an optimal threshold to separate foreground (potential tumor region) from background  
- **Morphological Operations**:
  - Erosion (removes small noise regions)  
  - Dilation (expands relevant regions)  
  - Hole filling (ensures continuous tumor region)  
- **Connected Component Analysis**: Identifies and selects the most likely tumor region based on size or location  

This step reduces the influence of irrelevant background regions and improves the quality of extracted features.

---

### 3. Feature Extraction

Feature extraction converts image data into numerical representations suitable for classification.

The following features are used:

- **Discrete Wavelet Transform (DWT)**:
  - Decomposes the image into multiple frequency subbands  
  - Captures texture variations at different scales  

- **Gray-Level Co-occurrence Matrix (GLCM)**:
  - Extracts spatial relationships between pixel intensities  
  - Captures structural patterns in the image  

- **Statistical Features**:
  - Mean  
  - Variance  
  - Entropy  

These features provide complementary information, combining both frequency-domain and spatial-domain characteristics of MRI images.

---

### 4. Classification

Classification is performed using:

- **Support Vector Machine (SVM)**:
  - Supervised learning algorithm  
  - Effective for moderate-sized feature vectors  
  - Both linear and radial basis function (RBF) kernels can be used  

The classifier is trained to distinguish between tumor and non-tumor images based on extracted features.

---

### 5. Evaluation

The performance of the system is evaluated by comparing the baseline and ROI-based pipelines using:

- Accuracy  
- Precision  
- Recall  
- F1-score  
- Confusion matrix  

Cross-validation or repeated hold-out validation is used to ensure reliable evaluation.
