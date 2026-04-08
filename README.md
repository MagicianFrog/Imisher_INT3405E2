# CAFA6 Protein Function Prediction

This repository presents our solution for the **CAFA6 Kaggle competition**, aiming to predict protein functions (GO terms) from protein sequences.

## Approach

We propose a hybrid pipeline that combines:

### 1. DIAMOND + K-NN Baseline

We use DIAMOND to perform fast sequence similarity search against the training database.

- For each query protein, retrieve top-k similar sequences  
- Apply K-Nearest Neighbors (K-NN) to aggregate GO labels from neighbors  
- Use similarity scores as weights for label voting  

This serves as a strong homology-based baseline.

---

### 2. Label Propagation

We further refine predictions using label propagation:

- Construct a similarity graph from DIAMOND results  
- Propagate labels from confident nodes to their neighbors  
- Smooth and enrich label distributions  

---

### 3. Deep Learning Models (MLP + CNN)

We train two neural models:

- **MLP**: uses engineered features derived from sequence similarity and statistics  
- **CNN**: operates on raw protein sequences to capture local motifs and patterns  

---

### 4. Final Ensemble

Final predictions are obtained by combining:

- DIAMOND + K-NN outputs  
- Label propagation results  
- MLP predictions  
- CNN predictions  

The ensemble improves robustness and overall performance.

---

## Summary

- DIAMOND + K-NN provides a strong similarity-based baseline  
- Label propagation improves label coverage  
- MLP and CNN capture complementary learned representations  
- Ensemble of all components yields the final submission  