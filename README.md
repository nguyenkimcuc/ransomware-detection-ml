# Machine Learning model for detecting ransomware transactions

## Project Introduction
Ransomware attacks have become one of the most serious cybersecurity threats in recent years, with Bitcoin often being the preferred payment method due to its pseudonymous nature. This project aims to develop a machine learning-based system capable of identifying suspicious Bitcoin transactions potentially related to ransomware activities. By leveraging various supervised learning algorithms and ensemble techniques, the system seeks to enhance transaction security and support early detection of illicit financial activities.

## Project Objectives
- To analyze Bitcoin transaction data and identify behavioral patterns commonly associated with ransomware payments.
- To implement and evaluate several supervised machine learning models for binary classification: legitimate vs. ransomware-related transactions.
- To develop advanced ensemble learning models by combining the strengths of multiple base classifiers through stacking techniques.
- To compare the performance of individual models and ensemble models based on key evaluation metrics such as accuracy, precision, recall, and F1-score.
- To build a scalable, data-driven detection framework that can be adapted for future transaction monitoring systems.

## Dataset
The dataset used in this project is the **BitcoinHeist Ransomware Address Dataset**, provided by the UCI Machine Learning Repository.  
You can access the dataset (https://archive.ics.uci.edu/dataset/526/bitcoinheistransomwareaddressdataset).

### Description:
This dataset contains a collection of Bitcoin transaction records associated with known ransomware attacks, as well as legitimate transactions. It was compiled by gathering publicly available Bitcoin addresses tied to ransomware campaigns, combined with data extracted from the Bitcoin blockchain.

### Key Details:
- **Number of records:** 2,912,615 transactions  
- **Number of features:** 10  
- **Label type:** Multi-class initially (different ransomware families + 'white' for legitimate), converted to binary labels for this project (1 = ransomware transaction, 0 = legitimate)

### Features:
| Feature             | Description                                                          |
|:--------------------|:---------------------------------------------------------------------|
| `address`            | Bitcoin address involved in the transaction                          |
| `year`               | Year when the transaction occurred                                   |
| `day`                | Day of the year (1-365) when the transaction occurred                |
| `length`             | Length of the address string                                         |
| `weight`             | PageRank score of the address in the Bitcoin transaction network     |
| `count`              | Number of transactions associated with the address                  |
| `looped`             | Indicates if the address is part of a transaction loop (0 or 1)      |
| `neighbors`          | Number of unique neighboring addresses                               |
| `income`             | Total incoming transaction amount to the address (in BTC)            |

### Notes:
- The original `label` field contains multiple ransomware family names (e.g., `cryptolocker`, `cryptxxx`, `locky`, etc.).  
- For this project, these labels were converted into **binary classification**:
  - `1` for ransomware-related transactions  
  - `0` for legitimate transactions (originally labeled as `white`)

This dataset offers a valuable real-world use case for applying machine learning in digital forensics and cryptocurrency transaction analysis.

## Models

The following machine learning models were developed and evaluated in this project:
### Individual Models:
- **Decision Tree Classifier**
- **Random Forest Classifier**
- **XGBoost (Extreme Gradient Boosting) Classifier**
- **LightGBM (Light Gradient Boosting Machine) Classifier**
- **CatBoost Classifier**

### Ensemble Models:

- **Ensemble Model 1:**  
  Base learners: `CatBoostClassifier`, `LGBMClassifier`, `RandomForestClassifier`, and `XGBClassifier`  
  Meta learner: `CatBoostClassifier`

- **Ensemble Model 2:**  
  Base learners: `CatBoostClassifier`, `LGBMClassifier`, `RandomForestClassifier`, and `XGBClassifier`  
  Meta learner: `Logistic Regression`

- **Ensemble Model 3:**  
  Base learners: `CatBoostClassifier`, `LGBMClassifier`, `RandomForestClassifier`, `ExtraTreesClassifier`, `MLPClassifier` (multi-layer perceptron neural network), and `Logistic Regression`  
  Meta learner: `CatBoostClassifier`

- **Ensemble Model 4:**  
  Base learners: `CatBoostClassifier`, `LGBMClassifier`, `RandomForestClassifier`, `ExtraTreesClassifier`, and `MLPClassifier`  
  Meta learner: `CatBoostClassifier`

---

**Notes:**  
All ensemble models were built using the stacking technique, where multiple base learners are trained independently and their predictions are combined by a meta-learner to make the final decision.

## Results
The evaluation process was divided into two stages: a model comparison phase and a final performance assessment of the selected model.

### Model Comparison on the Validation Set

Multiple machine learning models were trained and evaluated on a validation set using six key performance metrics:
- **Precision**
- **Recall**
- **F1-Score**
- **AUC-ROC**
- **PR AUC (Area Under the Precision-Recall Curve)**
- **Inference Time**

A series of comparison charts were created to visualize the performance of each model across these metrics.  

**Highlights:**
- **Ensemble Model 4** consistently outperformed other individual and ensemble models in terms of precision, recall, F1-score, AUC-ROC, and PR AUC, while maintaining a reasonable inference time.
- As a result, **Ensemble Model 4** was selected as the final model for further evaluation.

### Final Model Performance on the Test Set

The selected **Ensemble Model 4** was then tested on an unseen test set to assess its real-world performance.  

Performance visualization included:
- A **confusion matrix** showing true positives, true negatives, false positives, and false negatives.
  ![image](https://github.com/user-attachments/assets/9aa7ff19-4978-4e6a-bf57-6e6ab3b8e711)

- Classification Report:
  ![image](https://github.com/user-attachments/assets/0dd2cf88-29b6-4fa3-840b-cdddeac3510f)

- **Precision-Recall (PR) curve**
  ![image](https://github.com/user-attachments/assets/3ee86abc-44c7-4b18-a6b3-e0825e30c1d6)

**Summary:**
- The final model maintained high precision and recall on the test set, confirming its ability to accurately detect ransomware-related Bitcoin transactions while minimizing false alarms.
- The PR AUC and ROC AUC scores further validated the robustness of the model under class imbalance conditions.

