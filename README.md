---

# LeNet-5 Architecture 

This project implements the **exact original LeNet-5 architecture** as proposed by **Yann LeCun et al. (1998)** in the paper *“Gradient-Based Learning Applied to Document Recognition”*. The model is designed specifically for **handwritten digit recognition (e.g., MNIST dataset)** and is one of the earliest and most influential Convolutional Neural Networks (CNNs).

---

## 📐 Architecture Overview

LeNet-5 follows a **7-layer architecture** (excluding input), consisting of alternating **convolutional and subsampling (pooling) layers**, followed by fully connected layers.

```
Input (32×32)
   ↓
C1 → S2 → C3 → S4 → C5 → F6 → Output
```

Let’s break down **each layer in detail**.

---

## Input Layer

* **Input Size:** `32 × 32 × 1` (grayscale image)
* Although MNIST images are `28 × 28`, they are **padded to 32 × 32** to preserve edge information.

---

## C1 – Convolution Layer 1

* **Type:** Convolution
* **Filters:** 6
* **Kernel Size:** `5 × 5`
* **Stride:** 1
* **Output Size:** `28 × 28 × 6`
* **Parameters:** (5×5×1)×6 + 6 = **156**

### Purpose:

* Detects **basic features** such as edges, corners, and blobs.
* Each filter learns a different low-level feature.

---

## S2 – Subsampling Layer 1 (Average Pooling)

* **Type:** Average Pooling (not max pooling in original LeNet)
* **Kernel Size:** `2 × 2`
* **Stride:** 2
* **Output Size:** `14 × 14 × 6`

### Purpose:

* Reduces spatial dimensions
* Adds **translation invariance**
* Reduces computational cost

>  Note: Original LeNet uses **average pooling with trainable parameters**, not max pooling.

---

## C3 – Convolution Layer 2

* **Filters:** 16
* **Kernel Size:** `5 × 5`
* **Output Size:** `10 × 10 × 16`
* **Connections:** Not fully connected to all S2 maps (partial connection scheme)

### Purpose:

* Learns **more complex patterns** by combining features from C1.
* Detects shapes like curves, combinations of edges, etc.

---

## S4 – Subsampling Layer 2

* **Type:** Average Pooling
* **Kernel Size:** `2 × 2`
* **Stride:** 2
* **Output Size:** `5 × 5 × 16`

### Purpose:

* Further spatial reduction
* Keeps important features while discarding noise

---

## C5 – Convolution Layer 3 (Fully Connected Convolution)

* **Filters:** 120
* **Kernel Size:** `5 × 5`
* **Output Size:** `1 × 1 × 120`

### Why 1×1?

Because input is `5×5`, applying `5×5` filters collapses spatial dimension.

### Purpose:

* Acts like a **fully connected layer**
* Each neuron sees the **entire image**
* Learns high-level representations of digits

---

## F6 – Fully Connected Layer

* **Units:** 84

### Purpose:

* Combines all extracted features
* Learns **digit-specific patterns**
* 84 was chosen intentionally by LeCun (related to ASCII codes)

---

## Output Layer

* **Units:** 10
* **Activation:** Softmax
* **Represents:** Digits **0–9**

### Purpose:

* Produces probability distribution over 10 classes

---

## 📊 Layer-by-Layer Summary Table

| Layer  | Type           | Output Shape | Description            |
| ------ | -------------- | ------------ | ---------------------- |
| Input  | -              | 32×32×1      | Padded grayscale image |
| C1     | Conv (6×5×5)   | 28×28×6      | Low-level features     |
| S2     | Avg Pool       | 14×14×6      | Downsampling           |
| C3     | Conv (16×5×5)  | 10×10×16     | Complex features       |
| S4     | Avg Pool       | 5×5×16       | Downsampling           |
| C5     | Conv (120×5×5) | 1×1×120      | High-level features    |
| F6     | Dense (84)     | 84           | Feature combination    |
| Output | Dense (10)     | 10           | Digit classification   |

---

## Statement for README (Important)

You can **clearly claim** this in your README:

> **“This implementation strictly follows the original LeNet-5 architecture proposed by Yann LeCun et al., without structural modification. All layers, filter sizes, and design principles match the original paper.”**

Or shorter:

> **“This project implements the exact original LeNet-5 architecture.”**

---

## 💡 Why LeNet is Important

* First successful CNN in real-world application (bank cheque recognition)
* Introduced:

  * Convolution layers
  * Subsampling (pooling)
  * Weight sharing
  * Hierarchical feature learning
* Foundation of **AlexNet, VGG, ResNet, etc.**

---
