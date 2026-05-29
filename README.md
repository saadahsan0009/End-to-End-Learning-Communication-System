# End-to-End Learning of Communication Systems Using Deep Learning

> **MSc Electronic Engineering — University of Essex, Colchester, UK**
> **Awarded with Distinction | November 2022**
> **Supervisor: Dr. Varasteh, Morteza**

A deep learning-based autoencoder architecture designed to jointly optimise transmitter, channel, and receiver as a single end-to-end reconstruction task — replacing the traditional block-structured communication system.

---

## 📌 Problem Statement

Traditional communication systems are built as separate blocks — source coding, encryption, channel coding, modulation, and so on. Each block is optimised individually, which does not guarantee optimal end-to-end performance.

This project reframes communication between two devices as an **end-to-end reconstruction task**, replacing the conventional architecture with a single deep neural network trained to minimise bit error rate (BER) directly.

---

## 🎯 Key Results

| Configuration | Method | Performance |
|--------------|--------|-------------|
| Autoencoder (7,4) | Hybrid XGBoost | Matches Hamming (7,4) with MLD — outperforms uncoded BPSK and Hamming hard decision |
| Autoencoder (2,2) | Baseline | Identical performance to uncoded BPSK (2,2) |
| Autoencoder (8,8) | Higher order | Outperforms uncoded BPSK (8,8) — gap increases with higher Eb/N0 |
| Autoencoder (2,4) | Energy constrained | Rotated 16-PSK like constellation — competitive BER performance |

> The autoencoder demonstrates **equal or better BER performance** than traditional uncoded BPSK across all tested configurations, with performance advantage growing as message space size increases.

---

## 🏗️ System Architecture

The entire communication system is modelled as a fully connected feedforward neural network in **autoencoder configuration**:

```
Input Message (s)
      ↓
[TRANSMITTER]
  Dense + ReLU (M dimensions)
  Dense + Linear (n dimensions)
  Normalisation Layer
      ↓
[CHANNEL]
  Gaussian Noise Layer (AWGN simulation)
      ↓
[RECEIVER]
  Dense + ReLU (M dimensions)
  Dense + Softmax (M dimensions)
      ↓
Reconstructed Message (ŝ)
```

### Layer Summary

| Layer | Output Dimensions | Activation |
|-------|------------------|------------|
| Input | M | — |
| Dense | M | ReLU |
| Dense | n | Linear |
| Normalisation | n | — |
| Noise (AWGN) | n | — |
| Dense | M | ReLU |
| Dense | M | Softmax |

---

## ⚙️ Four Configurations Tested

| Config (n,k) | Bits per message (k) | Channel uses (n) | Rate R | Message space M |
|-------------|---------------------|-----------------|--------|-----------------|
| (2,2) | 2 | 2 | 1 | 4 |
| (2,4) | 4 | 2 | 2 | 16 |
| (7,4) | 4 | 7 | 4/7 | 16 |
| (8,8) | 8 | 8 | 1 | 256 |

**Training parameters:**
- SNR fixed at 7dB (Eb/N0 = 5.01187) during training
- Optimiser: Adam (learning rate = 0.001)
- Loss function: Categorical cross-entropy
- Training examples: 100,000 per configuration
- Testing range: Eb/N0 from -4 to 12 dB

---

## 🔍 Constellation Diagrams

The autoencoder learns its own signal representations — visualised through constellation diagrams:

- **(2,2):** QPSK-like constellation — 4 symbols arranged in quadrants
- **(2,4) energy constrained:** Rotated 16-PSK like arrangement
- **(2,4) power constrained:** Mixed pentagonal/hexagonal arrangement
- **(7,4) and (8,8):** Higher-dimensional representations visualised using t-SNE dimensionality reduction

These learned constellations emerge entirely from training — the network discovers optimal signal representations without being explicitly taught them.

---

## 💡 Key Findings

- Deep learning autoencoders can **match or outperform** traditional communication architectures without using expert-designed signal processing blocks
- Performance advantage grows with **larger message spaces and more channel uses**
- The architecture shows **flexibility across channel noise variance** even when trained at a fixed SNR — demonstrating adaptability beyond training conditions
- **Parallel processing architecture** of deep learning models offers lower latency and computational efficiency compared to traditional block-structured systems

---

## 🚀 Future Work

- Extend to **fading channel models** beyond AWGN
- Test in **non-ideal conditions** where traditional systems typically underperform
- Expand to **multi-user scenarios** with shared channel interference
- Larger message spaces with more bits per symbol

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.x-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)
![Keras](https://img.shields.io/badge/Keras-deep%20learning-red)
![NumPy](https://img.shields.io/badge/NumPy-numerical-lightblue)
![Matplotlib](https://img.shields.io/badge/Matplotlib-visualisation-green)

- **Framework:** TensorFlow / Keras
- **Language:** Python
- **Libraries:** NumPy, Matplotlib, Scikit-learn
- **Environment:** Jupyter Notebook / Google Colab

---

## 📁 Repository Structure

```
├── Dissertation_Report.pdf        # Full written dissertation
├── README.md                      # This file
```

> **Note:** The original training code is available at the linked repository from the dissertation period. This repo preserves the full research report and findings.

---

## 📚 Key References

- O'Shea, T. & Hoydis, J. (2017). *An Introduction to Deep Learning for the Physical Layer.* IEEE Transactions on Cognitive Communications and Networking, 3(4), 563–575.
- Dörner, S. et al. (2017). *Deep Learning Based Communication Over the Air.* IEEE Journal of Selected Topics in Signal Processing, 12(1), 132–143.

---

## 👤 Author

**Saad Ahsan**
MSc Electronic Engineering (Distinction) — University of Essex
MSc Data Science (Distinction) — Middlesex University London

📧 saadahsan0009@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/saad-ahsan-1901sam/)
🐙 [GitHub](https://github.com/saadahsan0009)

---

## 📄 Academic Context

This work was completed as the dissertation component of the MSc Electronic Engineering programme at the University of Essex, School of Computer Science and Electronics Engineering, August 2022. The degree was awarded with Distinction in November 2022.
