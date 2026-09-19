# 🏥 Surgical Vision: Phase & Tool Tracking

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Medical Imaging](https://img.shields.io/badge/Domain-Medical_Imaging-008080?style=for-the-badge)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)

A comprehensive computer vision pipeline designed to analyze laparoscopic and endoscopic surgical videos. This system simultaneously localizes surgical instruments (e.g., graspers, hooks, scissors) and predicts the current surgical phase (workflow step) in real-time. By combining spatial feature extraction with temporal sequence modeling, the framework provides critical context-awareness for modern computer-assisted surgical systems.

---

## ✨ Key Features

* **Surgical Tool Tracking:** Utilizes robust object detection backbones (`[e.g., YOLOv8 or Mask R-CNN]`) to detect and track the bounding boxes or segmentation masks of specific surgical tools despite motion blur and specular reflections.
* **Workflow Phase Recognition:** Employs temporal modeling (`[e.g., Temporal Convolutional Networks (TCN) or LSTMs]`) on extracted video frame features to classify the current step of the operation (e.g., Calot Triangle Dissection, Gallbladder Packaging).
* **Multi-Task Learning:** Shares a common visual feature extraction backbone for both spatial tool detection and temporal phase recognition, optimizing inference speed for real-time surgical deployment.
* **Temporal Smoothing:** Integrates Hidden Markov Models (HMM) or temporal constraints to prevent erratic jumps in phase predictions, ensuring logical workflow transitions.
* **Clinical Dashboard Overlay:** Generates an annotated video feed displaying tracked tool coordinates, confidence scores, and a live timeline of the surgical procedure.

---

## 🏗️ Pipeline Architecture

```text
                       +-----------------------------+
                       | Endoscopic Video Stream     |
                       +--------------+--------------+
                                      |
                                      v
                       +--------------+--------------+
                       | Spatial Feature Extractor   | (e.g., ResNet-50 / EfficientNet)
                       +------+---------------+------+
                              |               |
             +----------------+               +----------------+
             |                                                 |
             v                                                 v
+------------+------------+                      +-------------+------------+
| Tool Detection Head     |                      | Temporal Sequence Model  | (TCN / LSTM)
| (Bounding Boxes/Masks)  |                      | (Phase Classification)   |
+------------+------------+                      +-------------+------------+
             |                                                 |
             v                                                 v
+------------+------------+                      +-------------+------------+
| Instrument Coordinates  |                      | Current Surgical Phase   |
| & Identification        |                      | & Transition Timeline    |
+------------+------------+                      +-------------+------------+
             |                                                 |
             +-----------------------+-------------------------+
                                     |
                                     v
                       +-------------+-------------+
                       | Synchronized Video Output |
                       | (Clinical HUD)            |
                       +---------------------------+
