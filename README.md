# 🧠 PERG Retinal Disease Classification using Deep Learning
Author - Suyash Khare

A deep learning pipeline for retinal disease classification using Pattern Electroretinogram (PERG) signals from the IOBA-PERG dataset (PhysioNet).

This project investigates whether deep neural networks can automatically learn disease-specific patterns from retinal electrophysiological signals to assist in retinal diagnostics.

---

## 📊 Dataset

**Dataset:** IOBA-PERG  
**Source:** PhysioNet  

The dataset contains Pattern Electroretinogram (PERG) recordings collected from patients with different retinal and optic nerve disorders.

Each record includes:

- **RE** → Right Eye PERG signal  
- **LE** → Left Eye PERG signal  
- Sampling Frequency → **170 Hz**
- Clinical metadata including:
  - Age
  - Sex
  - Diagnosis labels

---

## 📁 Dataset Curation

The original dataset contains many rare diseases with very few samples.  
To reduce severe class imbalance, a curated subset of **10 clinically relevant diseases** was selected.

| Disease | Samples |
|-------|-------|
| Normal | 40 |
| Retinitis pigmentosa | 40 |
| Macular dystrophy | 40 |
| Stargardt disease | 34 |
| Cone-Rod dystrophy | 27 |
| Birdshot chorioretinopathy | 23 |
| Autoimmune retinopathy | 19 |
| Inherited optic atrophy | 17 |
| Congenital stationary night blindness | 14 |
| Retinal toxicity | 14 |

**Total Samples:** 268

To avoid patient leakage, **one session per patient was selected whenever possible.**

---

## 🧬 Signal Representation

Each PERG sample contains two electrophysiological time-series signals:

- Channel 1 → Right Eye PERG (RE)  
- Channel 2 → Left Eye PERG (LE)

Model input shape:

```
(batch_size, channels, time_steps)
channels = 2
```

---

## 🧠 Model Architecture

The project uses a **Deep 1D Convolutional Neural Network (CNN)** to learn temporal patterns from PERG signals.

### Architecture

```
Input (2 × T PERG signal)

↓ Conv1D + BatchNorm + ReLU
↓ MaxPooling

↓ Conv1D + BatchNorm + ReLU
↓ MaxPooling

↓ Conv1D + BatchNorm + ReLU
↓ MaxPooling

↓ Conv1D + BatchNorm + ReLU

↓ Global Average Pooling

↓ Fully Connected Layer

↓ Softmax Classifier
```

### Key Components

- Temporal feature extraction using **1D convolutions**
- **Batch normalization** for training stability
- **Global average pooling** to reduce overfitting
- **Dropout regularization**

---

## ⚙️ Training Strategy

Training was implemented using **PyTorch**.

**Loss Function**

Cross Entropy Loss with class weighting to address dataset imbalance.

**Optimizer**

Adam Optimizer

**Evaluation Metrics**

- Accuracy  
- Macro F1 Score

---

## 📂 Repository Structure

```
PERG-Retinal-Disease-Classification

│
├── main.ipynb
│   End-to-end training pipeline
│
├── models
│   Deep CNN architecture
│
├── data_processing
│   Dataset preparation scripts
│
├── PERG_selected_dataset
│   Curated dataset used for training
│
└── results
    Training curves and evaluation results
```

---

## 📈 Applications

Potential applications include:

- AI-assisted retinal disease diagnosis
- Automated electroretinography signal analysis
- Ophthalmology research tools
- Early detection of retinal degeneration

---

## 🔬 Future Work

Possible future extensions:

- Transformer-based time-series models
- Cross-patient validation strategies
- Explainable AI for PERG interpretation
- Expansion to additional retinal diseases

---

## 📜 License

This repository is intended for **research and educational purposes**.
