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
