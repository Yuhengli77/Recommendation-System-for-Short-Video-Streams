# Project Proposal: Two-Stage Sequential Recommendation System for Short-Video Streams

## 1. Introduction and Motivation

With the explosive growth of short-video platforms such as TikTok and Kuaishou, building scalable and accurate recommendation systems has become a critical challenge in industrial recommender system design. Unlike traditional recommendation tasks, short-video consumption exhibits strong **sequential and temporal dependencies** — users’ next viewing behavior depends heavily on their immediate past interactions.

This project aims to design and implement a **two-stage recommendation system (Recall + Ranking)** tailored for large-scale short-video scenarios. Using the **KuaiSAR dataset** released by Kuaishou, we will conduct a complete experimental pipeline — from exploratory data analysis (EDA) to model implementation, evaluation, and comparison — to validate the effectiveness of **Transformer-based sequential models** in next-item prediction tasks.

---

## 2. Dataset and Exploratory Analysis

### 2.1 Dataset Description

- **Dataset:** KuaiSAR (Kuaishou Sequential and Attentive Recommendation)  
- **Source:** Released by Kuaishou, representing real-world user–item interaction sequences.  
- **Characteristics:** Large-scale, sparse, and temporally ordered user behavior data, suitable for studying sequential recommendation.  
- **Core Features:**  
  - `user_id`, `item_id`, `timestamp`  
  - Implicit feedback data (watch or skip behavior)

### 2.2 Exploratory Data Analysis (EDA)

We will conduct systematic EDA to guide model design decisions:

- **User Behavior Sequence Length Distribution** – Identify session length statistics and typical user engagement patterns.  
- **Item Popularity Distribution** – Examine long-tail effects in content interaction frequencies.  
- **Temporal Interaction Analysis** – Explore user engagement trends across time (e.g., hourly or daily patterns).

**Expected Insights:**  
EDA results are expected to reveal strong sequential dependencies and a vast, sparse item space — highlighting the necessity of a **multi-stage recommendation architecture** that balances efficiency and precision.

---

## 3. Task Definition and Baseline Setup

### 3.1 Problem Formulation

**Task:** *Next-Item Prediction*  
Given a user’s interaction sequence \( S_u = \{v_1, v_2, ..., v_t\} \), predict the next item \( v_{t+1} \) the user is most likely to interact with.

### 3.2 Evaluation Protocol

- **Data Splitting:** Leave-One-Out strategy — the last item in each user sequence is reserved for testing.  
- **Metrics:**  
  - **Hit Rate @ K (HR@K):** Measures whether the ground-truth next item appears in the top-K list.  
  - **NDCG @ K (Normalized Discounted Cumulative Gain):** Evaluates ranking quality by emphasizing higher-ranked correct predictions.

### 3.3 Baseline Models

We will establish several baseline models for performance comparison:

| Model | Description | Notes |
|--------|--------------|-------|
| **MostPopular** | Recommends globally most popular items | Non-personalized |
| **ItemCF** | Item-based collaborative filtering using co-occurrence signals | Simple, fast collaborative baseline |
| **NeuMF** | Neural matrix factorization combining GMF and MLP components | Captures nonlinear user–item interactions |

---

## 4. System Design and Model Architecture

### 4.1 Two-Stage Framework

To address the scalability–accuracy trade-off in large-scale recommendation, we adopt a **two-stage pipeline**:
1. **Recall Stage:** Efficiently retrieves hundreds of candidate items from millions.  
2. **Ranking Stage:** Applies a deep sequential model for fine-grained scoring.

This design mirrors architectures used in industrial systems (e.g., YouTube, Alibaba).

### 4.2 Recall Stage

- **Method:** Deep Structured Semantic Model (DSSM) that learns user and item embeddings for approximate nearest-neighbor retrieval.  
- **Advantages:** Captures richer representation similarities than heuristic CF while remaining retrieval-efficient through embedding search.  
- **Output:** A compact candidate pool for ranking.

### 4.3 Ranking Stage

- **Model:** **SASRec (Self-Attentive Sequential Recommendation)**  
- **Motivation:** SASRec leverages Transformer self-attention to capture **long-range dependencies** in user behavior sequences, outperforming RNN-based methods in accuracy and interpretability.  
- **Optimization:**  
  - Optimizer: *Adam*  
  - Regularization: *Dropout* and *L2 weight decay*  
  - Loss: *Binary cross-entropy* or *pairwise ranking loss*

---

## 5. Related Work

We will perform a literature review to contextualize the design choices.

1. **Dataset and Benchmarks**  
   - KuaiSAR dataset release paper describing data construction and benchmark tasks.

2. **Industrial Two-Stage Architectures**  
   - Covington et al., *“Deep Neural Networks for YouTube Recommendations”*, RecSys 2016.  
   - Zhou et al., *“Deep Interest Network for Click-Through Rate Prediction”*, KDD 2018.  
   - Huang et al., *“Learning Deep Structured Semantic Models for Web Search”*, CIKM 2013.

3. **Recommendation Models**  
   - Sarwar et al., *“Item-Based Collaborative Filtering Recommendation Algorithms”*, WWW 2001.  
   - He et al., *“Neural Collaborative Filtering”*, WWW 2017.  
   - Kang & McAuley, *SASRec: Self-Attentive Sequential Recommendation*, ICDM 2018.

These works collectively support our two-stage architecture and motivate the use of Transformer-based sequence modeling.

---

## 6. Experimental Results and Analysis

### 6.1 Quantitative Results

Performance will be evaluated using HR@K and NDCG@K metrics.  
Results will be summarized in tables and visualized with bar or line plots comparing:
- **Baselines:** MostPopular, ItemCF, NeuMF  
- **Proposed Model:** SASRec

### 6.2 Qualitative and Case Studies

We will conduct case studies by visualizing attention distributions for selected users, illustrating how SASRec identifies relevant historical behaviors compared to baselines.

### 6.3 Discussion

We expect SASRec to significantly outperform non-sequential collaborative baselines such as ItemCF and NeuMF, confirming the benefit of self-attention in capturing contextual dependencies.  
Error analysis will also explore challenges such as cold-start users and popularity bias.

---

## 7. Conclusion and Future Work

This project demonstrates the feasibility and effectiveness of applying **Transformer-based sequential modeling** within a **two-stage architecture** for short-video recommendation.  
Our findings will provide insights into the trade-offs between efficiency and accuracy in large-scale recommender systems.

**Future Directions:**
- Incorporate **content-aware embeddings** (text, audio, and video features).  
- Explore **ANN-based hybrid recall** (e.g., FAISS or pgvector retrieval).  
- Extend to **online simulation settings** using reinforcement learning for ranking optimization.

---

## 8. Expected Deliverables

| Deliverable | Description |
|--------------|-------------|
| **EDA Report** | Statistical and visual analysis of KuaiSAR dataset |
| **Baseline Implementations** | MostPopular, ItemCF, NeuMF |
| **SASRec Model** | Transformer-based ranking module |
| **Evaluation Report** | Quantitative and qualitative results |
| **Final Report & Presentation** | Comprehensive summary of methodology, results, and insights |

---

## 9. References

- Kang, W., & McAuley, J. (2018). *Self-Attentive Sequential Recommendation*. ICDM.  
- Covington, P. et al. (2016). *Deep Neural Networks for YouTube Recommendations*. RecSys.  
- Zhou, G. et al. (2018). *Deep Interest Network for Click-Through Rate Prediction*. KDD.  
- Huang, P.-S. et al. (2013). *Learning Deep Structured Semantic Models for Web Search*. CIKM.  
- Sarwar, B. et al. (2001). *Item-Based Collaborative Filtering Recommendation Algorithms*. WWW.  
- He, X. et al. (2017). *Neural Collaborative Filtering*. WWW.  
- KuaiSAR Dataset: [https://kuaisar.github.io/](https://kuaisar.github.io/)

---
