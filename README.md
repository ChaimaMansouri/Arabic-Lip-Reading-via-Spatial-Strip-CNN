# 🎥 Arabic Lip Reading via Spatial Strip CNN

A deep learning project for **Arabic visual speech recognition** that recognizes spoken Arabic phrases from silent videos using only lip movements.

The project introduces a **Spatial Strip** representation that transforms temporal lip movements into a 2D image, which is then classified using a custom **2D Convolutional Neural Network (CNN)**.

---

## 🎯 Project Overview

The system converts Arabic speech videos into visual representations of lip movements and classifies them into **10 Arabic phrase categories**.

### System Pipeline

```text
Arabic Video
      ↓
Face Detection
      ↓
Lip Region Extraction
      ↓
15 Sampled Frames
      ↓
64 × 64 Lip Images
      ↓
Spatial Strip (64 × 960)
      ↓
2D CNN
      ↓
10 Arabic Phrases
```

---

## 🗂️ Dataset

The project uses the **LRC-AR Dataset from Al Jazeera Arabic**.

After selecting the **10 most frequent phrases**, the working dataset contains:

- **561 videos**
- **10 Arabic phrase classes**
- **448 training samples**
- **113 validation samples**

The data is divided using a **stratified 80/20 train-validation split**.

### Phrase Classes

| ID | Arabic Phrase |
|---:|---|
| 0 | السلام عليكم |
| 1 | أهلاً بكم إلى موجز |
| 2 | أفاد مراسل الجزيرة |
| 3 | موجز الأنباء من قناة |
| 4 | إلى اللقاء |
| 5 | قال مراسل الجزيرة |
| 6 | نهاية الموجز إلى اللقاء |
| 7 | ميليشيا الحوثي وقوات |
| 8 | قالت مصادر |
| 9 | من جهته قال |

---

## 👄 Lip Region Extraction

The system uses **OpenCV Haar Cascade** for face detection and extracts the mouth region from the detected face.

For each video:

- **15 frames** are sampled.
- Each lip region is resized to **64 × 64** pixels.
- The frames are concatenated horizontally.
- The resulting Spatial Strip has a size of **64 × 960**.

This representation converts the temporal evolution of lip movements into a single 2D image.

---

## 🔄 Data Processing

The preprocessing pipeline includes:

- Video loading using OpenCV
- Face detection
- Lip region extraction
- Grayscale conversion
- Frame sampling
- Image resizing
- Spatial Strip generation
- Normalization

The generated dataset has the following shape:

```text
X: (561, 1, 64, 960)
y: (561,)
```

---

## 🧪 Data Augmentation

Training data is augmented using:

- Random horizontal flipping
- Random brightness and contrast variation
- Random noise
- Random erasing
- Slight random rotation
- Random resizing and zooming

A **WeightedRandomSampler** is also used to address class imbalance during training.

---

## 🧠 Model

The project uses a custom **2D Convolutional Neural Network (CNN)** designed for the Spatial Strip representation.

### Input

```text
1 × 64 × 960
```

The CNN uses convolutional blocks with:

- Convolution
- Batch Normalization
- ReLU activation
- Max Pooling

The final feature representation is reduced using:

```text
AdaptiveAvgPool2d((4, 8))
```

The classifier produces predictions for the **10 Arabic phrase classes**.

---

## ⚙️ Training Configuration

| Parameter | Value |
|---|---|
| Model | Custom 2D CNN |
| Input Size | `1 × 64 × 960` |
| Number of Classes | 10 |
| Batch Size | 16 |
| Optimizer | AdamW |
| Learning Rate | `3e-4` |
| Weight Decay | `1e-4` |
| Loss Function | Cross-Entropy Loss |
| Label Smoothing | 0.1 |
| Scheduler | Cosine Annealing |
| Early Stopping | Yes |
| Random State | 42 |

---

## 📈 Results

The model achieved:

### **77.0% Validation Accuracy**

The evaluation includes:

- Validation accuracy
- Confusion matrix
- Per-class accuracy
- Training and validation curves

The model is evaluated on the held-out validation set.

---

## 🛠️ Technologies

- **Python**
- **PyTorch**
- **OpenCV**
- **NumPy**
- **Pandas**
- **Scikit-learn**
- **Matplotlib**
- **Seaborn**
- **Google Colab**
- **Google Drive**

---


## ▶️ How to Run

The project is implemented in a **Jupyter Notebook** and is designed to run in **Google Colab**.

The dataset is accessed through Google Drive. After configuring the dataset path, run the notebook cells sequentially to:

1. Load and index the videos.
2. Select the target phrase classes.
3. Extract lip regions.
4. Generate Spatial Strips.
5. Create the training and validation sets.
6. Train the CNN.
7. Evaluate the model.
8. Generate the evaluation visualizations.

---

## ⚠️ Limitations

- The current dataset contains 561 videos across 10 phrase classes.
- Evaluation is performed using a train-validation split.
- The system is limited to the selected 10 Arabic phrases.
- The approach relies on face detection and a predefined lip-region extraction method.
- Similar lip movements can lead to classification errors.

---

## 🔮 Future Work

- Expand the number of Arabic phrases.
- Increase dataset size and diversity.
- Improve lip-region detection and alignment.
- Explore advanced CNN architectures.
- Compare the Spatial Strip approach with 3D and temporal models.

---

## 📚 References

- **LRC-AR Dataset — Al Jazeera Arabic**
- **OpenCV**
- **PyTorch**
- **Scikit-learn**

---

## 👥 Team

- **Chaima Mansouri**
- **Nour El imene Houadji**
- **Chahd Touabia**


---


## 👩‍💻 Project

**Arabic Lip Reading via Spatial Strip CNN**

A visual speech recognition approach that transforms temporal lip movements into a 2D Spatial Strip for Arabic phrase classification.
