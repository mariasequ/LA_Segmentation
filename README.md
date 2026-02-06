# Automatic Left Atrium Segmentation using U-Net 🫀

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.X-orange)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-green)
![Status](https://img.shields.io/badge/Status-Educational%20%2F%20Portfolio-yellow)

## 📌 Project Overview
This project implements a Deep Learning pipeline to automatically segment the **Left Atrium** from medical CT scans (Computed Tomography). Accurate segmentation of the atrium is a critical step in the clinical workflow for diagnosing atrial fibrillation (AFib) and planning catheter ablation procedures.

Using a custom implementation of the **U-Net architecture**, the model learns to map input CT slices to binary segmentation masks, distinguishing the atrium tissue from the background.

## 🧠 Model Architecture
The model is based on the classic U-Net architecture (Ronneberger et al.), designed specifically for biomedical image segmentation.

### 1. Encoder (The Contracting Path)
* **Input:** 256x256 Grayscale CT slices.
* **Structure:** 3 blocks of double `Conv2D` layers followed by `MaxPooling2D`.
* **Filters:** Increasing depth (16 $\rightarrow$ 32 $\rightarrow$ 64) to capture high-level semantic features.
* **Activation:** ReLU (Rectified Linear Unit) for non-linearity.

### 2. Bottleneck
* The deepest layer of the network (128 filters).
* Includes **Dropout (0.2)** to prevent overfitting, forcing the model to learn robust generalized features rather than memorizing training data.

### 3. Decoder (The Expanding Path)
* **Structure:** Upsampling using `Conv2DTranspose` to restore spatial resolution.
* **Skip Connections:** Concatenates feature maps from the Encoder to the Decoder. This preserves fine-grained details (edges) lost during pooling, resulting in sharper segmentation masks.
* **Output Layer:** A `Sigmoid` activation function to output a probability map (0 to 1) for each pixel.

## 📊 Metrics & Loss Function
Since medical datasets are often imbalanced (the background is much larger than the organ), standard accuracy is not a reliable metric.

* **Loss Function:** `Binary Crossentropy`.
* **Evaluation Metric:** **Dice Coefficient** (F1 Score). This measures the overlap between the predicted mask and the ground truth, ignoring the background.

$$Dice = \frac{2 \times |Y_{true} \cap Y_{pred}|}{|Y_{true}| + |Y_{pred}|}$$

## 📁 Dataset & Preprocessing
* **Data Structure:** The dataset consists of 2D slices extracted from 3D CT volumes.
* **Preprocessing Pipeline:**
    * **Grayscale Conversion:** Simplifies input to density maps.
    * **Normalization:** Pixel intensity scaled to range `[0, 1]`.
    * **Reshaping:** inputs adapted to `(N, 256, 256, 1)` tensors.

*> **Note:** The actual medical images are not included in this repository due to privacy and licensing restrictions.*

## 🚀 Results
*(You can update this section with your training graphs)*

* **Training Dice Score:** `[POSA EL TEU RESULTAT AQUÍ, EX: 0.92]`
* **Validation Dice Score:** `[POSA EL TEU RESULTAT AQUÍ, EX: 0.88]`

### Visual Sample
Below is a comparison showing the Input CT, the Radiologist's Mask (Ground Truth), and the U-Net's Prediction:

![Segmentation Result](images/results_sample.png)
*(Make sure to add a screenshot of your plot named 'results_sample.png' inside an 'images' folder)*

## 🛠️ Installation & Usage

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/YOUR_USERNAME/LA_Segmentation.git](https://github.com/YOUR_USERNAME/LA_Segmentation.git)
   cd LA_Segmentation
