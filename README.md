# Duplicate Question Pairs Detection

This project focuses on detecting **duplicate question pairs** — determining if two questions essentially ask the same thing (like Quora’s Duplicate Question Problem).

---

##  Project Overview

We applied the following pipeline:

###  Preprocessing:
- Lowercasing text
- Removing HTML tags
- Expanding chat slang (e.g., `BRB → Be Right Back`)
- Number normalization (`2 → two`)
- Spelling correction using **SymSpell**

###  Feature Engineering:
- **Basic Features:**  
  - Length of questions  
  - Word count  
  - Common & unique word ratios
- **Token-Based Features:**  
  - Non-stopword overlap  
  - Stopword overlap  
  - First/last word matches
- **Fuzzy Matching Features:**  
  - QRatio, Partial Ratio, Token Sort, and Token Set ratios using `fuzzywuzzy`
- **Vector-Based Features:**  
  - Bag-of-Words using `CountVectorizer`  
  - Average Word2Vec embeddings (150D per question)

---

##  Models Used
We tested three models:

| Model               | Accuracy |
|--------------------|----------|
| Logistic Regression | **75.66%**  |
| Random Forest       | ~72%     |
| XGBoost             | ~70%     |

---

##  Hyperparameter Tuning

We performed hyperparameter tuning using `GridSearchCV` to improve model performance and stability.

### Tuned Parameters:
- **Random Forest:** `n_estimators`, `max_depth`, `min_samples_split`, `min_samples_leaf`
- **Logistic Regression:** `C`, `penalty`
- **XGBoost:** `learning_rate`, `n_estimators`, `max_depth`

### Result:
Model accuracy improved by **~2–3%** after tuning:

| Model               | Accuracy (Before) | Accuracy (After Tuning) |
|--------------------|------------------|--------------------------|
| Logistic Regression | ~73%             | **75.66%**             |
| Random Forest       | ~69%             | ~72%                     |
| XGBoost             | ~68%             | ~70%                     |

---

