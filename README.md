# 🍅 Tomato Image Retrieval using Global Features and CBIR

**Content-Based Image Retrieval (CBIR) using Color, Shape, and Texture Features**

A computer vision project that implements a **Content-Based Image Retrieval (CBIR)** system to retrieve visually similar tomato images based on their visual characteristics.

The system analyzes tomato images using global feature extraction, including color distributions, geometric properties, and texture patterns. These features are used to measure image similarity and rank the most relevant images from a database.

This project was developed as part of the **Digital Image Processing (Pengolahan Citra Digital)** coursework at Universitas Brawijaya.

---

## 📌 Project Overview

Traditional image retrieval often relies on textual descriptions or manually assigned labels. In contrast, **Content-Based Image Retrieval (CBIR)** retrieves images by analyzing their visual content.

This project focuses on retrieving tomato images based on three main characteristics:

- **Color:** Identifying similarities in tomato colors and their distributions.
- **Shape:** Comparing geometric characteristics of tomato objects.
- **Texture:** Analyzing pixel intensity patterns on tomato surfaces.

The system processes a query image and compares its extracted features with those of images stored in a database.

## 🎯 Objectives

1. Implement tomato object segmentation to separate foreground objects from their backgrounds.
2. Extract global image features representing color, shape, and texture.
3. Apply feature normalization to make different feature scales comparable.
4. Calculate similarity between query images and database images.
5. Rank database images based on their similarity scores.
6. Evaluate retrieval results through visual observation and feature analysis.

## 🔄 System Workflow

The CBIR system consists of the following stages:

```text
          TOMATO IMAGE DATASET
                   |
                   v
           Image Segmentation
                   |
                   v
         Global Feature Extraction
                   |
          +--------+--------+
          |        |        |
        Color     Shape    Texture
          |        |        |
          +--------+--------+
                   |
                   v
        Feature Representation
                   |
                   v
         Feature Normalization
                   |
                   v
          Feature Weighting
                   |
                   v
          Distance Calculation
                   |
                   v
          Similarity Ranking
                   |
                   v
        TOP-K SIMILAR IMAGES
```

Both database images and query images undergo segmentation and feature extraction. The extracted features are then compared to identify the most similar images.

## 🗂️ Dataset

The dataset consists of **7 tomato images**, divided into:

| Category | Number of Images | Purpose |
|---|---:|---|
| Database Images | 5 | Reference images for similarity comparison |
| Query Images | 2 | Input images used for retrieval |
| **Total** | **7** | |

The images contain variations in tomato color, ripeness, shape, number of objects, and background conditions.

These variations are intended to evaluate how different visual characteristics affect image retrieval.

## 🔍 Image Segmentation

Image segmentation is performed to isolate tomato objects from their backgrounds before extracting visual features.

The segmentation process uses image processing techniques such as:

- HSV color thresholding
- Morphological operations
- Sobel edge detection
- Watershed segmentation

The resulting binary masks identify foreground pixels corresponding to tomato objects.

Feature extraction is performed using the segmented object regions to reduce background interference.

## 🧠 Global Feature Extraction

The system extracts **21 global features** across three categories.

### 1. Color Features (15 Features)

Color features describe the distribution and variation of colors within the segmented tomato regions.

| Feature | Dimensions | Description |
|---|---:|---|
| Mean RGB | 3 | Average intensity of red, green, and blue channels |
| Standard Deviation RGB | 3 | Variation of RGB channel intensities |
| HSV Hue Histogram | 9 | Distribution of hue values across nine histogram bins |
| **Total** | **15** | |

Color features are useful for distinguishing red, yellow, orange, and green tomatoes.

### 2. Shape Features (3 Features)

Shape features represent the geometric properties of segmented tomato objects.

| Feature | Description |
|---|---|
| Area Ratio | Proportion of foreground pixels relative to the image area |
| Aspect Ratio | Ratio between the width and height of the object's bounding box |
| Circularity | Measurement of how closely an object's shape resembles a circle |

Circularity is calculated using:

**Circularity = 4πA / P²**

Where:

- A = Object area
- P = Object perimeter

These features help distinguish objects based on their size proportions, elongation, and geometric characteristics.

### 3. Texture Features (3 Features)

Texture features are extracted using the **Gray-Level Co-occurrence Matrix (GLCM)**.

| Feature | Description |
|---|---|
| Contrast | Measures local intensity differences |
| Homogeneity | Measures similarity between neighboring pixel intensities |
| Energy | Measures the concentration of intensity-pair distributions |

GLCM features help represent texture patterns that may not be captured by color and shape features alone.

### Feature Summary

| Feature Category | Number of Features |
|---|---:|
| Color | 15 |
| Shape | 3 |
| Texture | 3 |
| **Total** | **21** |

## 📊 Feature Normalization and Similarity Ranking

Since extracted features have different numerical ranges, normalization is applied before similarity comparison.

Feature weighting is used to control the contribution of each feature category to the overall similarity measurement.

The retrieval process follows these steps:

1. Extract feature vectors from database and query images.
2. Normalize the feature values using consistent normalization parameters.
3. Apply the selected feature weights.
4. Calculate distances between query and database feature vectors.
5. Sort database images by distance in ascending order.
6. Display the most similar images.

**A smaller distance indicates greater similarity according to the selected features and weights.**

## 🧪 Additional Experiment: ORB Feature Matching

An additional experiment explores local feature extraction using **ORB (Oriented FAST and Rotated BRIEF)**.

The experiment involves:

1. Selecting one tomato image.
2. Rotating the image by approximately 20 degrees.
3. Detecting keypoints and extracting ORB descriptors from both images.
4. Matching descriptors using BFMatcher with Hamming distance.
5. Visualizing corresponding keypoints.

This experiment demonstrates how local image features can help identify corresponding visual structures even after image rotation.

The ORB experiment is separate from the global-feature CBIR ranking pipeline.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| OpenCV | Image processing, segmentation, and feature detection |
| NumPy | Numerical operations |
| Pandas | Feature data management and analysis |
| Matplotlib | Image and feature visualization |
| scikit-image | Texture feature extraction using GLCM |
| Google Colab / Jupyter Notebook | Development and experimentation |

## 📁 Repository Structure

```text
Tomato-Image-Retrieval-CBIR/
│
├── Dataset/
│   ├── db_1_4tomat_merah.jpg
│   ├── db_2_tomat_kuning.jpg
│   ├── db_3_tomat_6buah.jpg
│   ├── db_4_tomat_oren.jpeg
│   ├── db_5_tomat_merah_hijau.jpg
│   ├── query_1_tomat_merah_mengkilat.jpg
│   └── query_2_tomat_kuning_kecil.jpeg
│
├── Ekstraksi_Fitur_Global_dan_Content_Based_Image_Retrieval_(CBIR).ipynb
├── Ekstraksi_Fitur_Global_dan_Content_Based_Image_Retrieval_(CBIR).pdf
│
└── README.md
```

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/frqXoXo/Tomato-Image-Retrieval-CBIR.git
```

### 2. Navigate to the Project Directory

```bash
cd Tomato-Image-Retrieval-CBIR
```

### 3. Install Dependencies

```bash
pip install opencv-python numpy pandas matplotlib scikit-image
```

### 4. Open the Notebook

Open the `.ipynb` file using Jupyter Notebook, Visual Studio Code, or Google Colab.

### 5. Configure the Dataset Path

Update the dataset directory path in the notebook according to your local or Google Drive environment.

### 6. Run the Notebook

Execute the notebook cells sequentially to perform image segmentation, feature extraction, normalization, and image retrieval.

## ⚠️ Limitations

This project has several limitations:

- **Small dataset:** Only five database images are used, limiting the diversity of retrieval results.
- **Segmentation sensitivity:** Complex backgrounds, lighting conditions, and overlapping objects can affect segmentation quality.
- **Feature dependency:** Retrieval results depend on the selected features, normalization method, and feature weights.
- **Global feature limitations:** Global descriptors do not fully represent detailed spatial relationships between objects.
- **Limited evaluation:** A small number of query images makes it difficult to generalize retrieval performance.

Future improvements could include expanding the dataset, improving segmentation, experimenting with alternative similarity metrics, and incorporating deep learning-based feature representations.

## 👨‍💻 Author

**Faruqi Akbar**

Informatics Engineering Student  
Faculty of Computer Science (FILKOM)  
Universitas Brawijaya

GitHub: [@frqXoXo](https://github.com/frqXoXo)

---

*Developed for educational purposes as part of the Digital Image Processing coursework at Universitas Brawijaya.*
