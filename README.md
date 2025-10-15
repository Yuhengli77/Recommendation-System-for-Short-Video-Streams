# Two-Stage-Sequential-Recommendation-System-for-Short-Video-Streams

# 🎬 Two-Stage Sequential Recommendation for Short-Video Streams

> Industrial-style **Recall + Ranking** pipeline for next-item prediction on short-video platforms, built on the **KuaiSAR** dataset and **Transformer-based** sequential models.

---

## 📘 What We’re Building

We implement an **industrial two-stage recommender system** tailored for short-video feeds:

1) **Recall Stage** — Efficiently retrieves a few hundred candidate videos from a very large catalog.  
2) **Ranking Stage** — Applies a **Transformer (SASRec)** sequential model to score and order candidates based on user history.

This repo demonstrates **how modern short-video recommenders are engineered end-to-end**: from data processing and EDA-driven design to a production-style two-stage architecture.

---

## 🎯 Project Goals

- **Reproduce** a scalable **two-stage** pipeline common in industry (YouTube-/Alibaba-style).
- **Model** user **sequential behaviors** for next-item prediction in short-video scenarios.
- **Showcase** a clean, extensible codebase for **rapid iteration** (data → recall → ranking).
- **Provide** strong defaults and modular interfaces (swap recall/ranking easily).

---

## ⚙️ Models

### Recall Stage (fast candidate generation)
- **ItemCF**: item–item similarity from co-occurrence.
- **BPR-MF embeddings**: nearest neighbors via embedding similarity.
- **Optional ANN**: FAISS / pgvector for scalable retrieval.

**Output**: A compact **candidate set** per user (e.g., top-200).

### Ranking Stage (precision scoring)
- **SASRec** (*Self-Attentive Sequential Recommendation*):
  - **Transformer self-attention** for long-range dependencies.
  - Robust to varying sequence lengths, interpretable via attention.
- **Optimization**:
  - Optimizer: **Adam**
  - Regularization: **Dropout**, **L2 weight decay**
  - Loss: **Binary cross-entropy** or **pairwise ranking loss**





