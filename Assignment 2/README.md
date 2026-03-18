# Fake News Detection – Text Classification Assignment 2

**Student:** Marcela Lozano  
**Date:** March 22nd 2026  
**Dataset:** Fake and Real News Dataset

---

# Project Overview

This project builds a machine learning system to classify news articles as **FAKE** or **REAL** using natural language processing techniques.

The task is a **binary text classification problem**, where the goal is to identify misinformation by analyzing linguistic patterns in news articles.

Several feature engineering techniques and machine learning models were tested and compared to determine the most effective approach for detecting fake news.

---

# Dataset Details

**Source:** Fake and Real News Dataset (commonly used for NLP classification tasks)
https://www.kaggle.com/datasets/clmentbisaillon/fake-and-real-news-dataset

The dataset contains two labeled categories:

- **FAKE news articles**
- **REAL news articles**

After combining the datasets:

| Class | Count |
|------|------|
| FAKE | 23,481 |
| REAL | 21,417 |

**Total articles:** ~44,898

The dataset includes the full text of each article which was used as the primary feature for classification.

The class distribution is relatively balanced, which helps ensure models do not become biased toward a single label.

---

# Feature Engineering

Two text feature engineering approaches were tested:

### TF-IDF Vectorization
TF-IDF represents text as weighted numerical vectors where words that are frequent in a document but rare across the dataset receive higher importance.

Advantages:
- Highlights informative words
- Works well with linear classifiers
- Often improves text classification performance

### Count Vectorization
Count Vectorization represents text using simple word frequency counts.

Advantages:
- Simpler representation
- Computationally efficient
- Works well with probabilistic models such as Naive Bayes

Vocabulary size was limited to a reasonable range to reduce noise and computational cost.

---

# Best Model Results

The best performing model was **Linear Support Vector Machine (SVM) with TF-IDF features**.

### Performance Metrics

| Metric | Score |
|------|------|
| Accuracy | 0.9949 |
| Precision | 0.9962 |
| Recall | 0.9940 |
| F1 Score | **0.9951** |

These results indicate that the model performs extremely well in distinguishing between fake and real news articles.

---

# Important Class (FAKE) Performance

Detecting **fake news** is the most important classification objective because missing fake articles (false negatives) allows misinformation to spread.

The Linear SVM model demonstrated strong performance for the FAKE class with very high precision and recall, indicating the model is both:

- Effective at detecting fake news
- Careful not to incorrectly classify real news as fake

This balance is captured by the high **F1 score**, which was used as the primary evaluation metric.

---

# Model Comparison

Three models were evaluated across five criteria.

| Model | Accuracy / F1 | Speed | Important Class Performance | Interpretability | Ease of Tuning |
|------|------|------|------|------|------|
| Logistic Regression + TF-IDF | Very High (F1 ≈ 0.988) | Fast | Very strong balance | High | Easy |
| Naive Bayes + CountVectorizer | High (F1 ≈ 0.959) | Very Fast | Good but slightly lower recall | Medium | Very Easy |
| Linear SVM + TF-IDF | **Highest (F1 ≈ 0.995)** | Fast | Best balance of precision and recall | Medium–Low | Moderate |

---

# Custom Inference Summary

To test how well the final model generalizes to new examples, **20 custom news headlines were created** including:

- Easy examples
- Trickier examples
- Different context examples

The model correctly classified:

**11 / 20 examples**

### Key Findings

- The model performs well on clearly fake or clearly legitimate news.
- Some difficult examples are harder to classify when language resembles legitimate journalism.
- This highlights the challenge of detecting misinformation when writing styles overlap.

---

# Recommendation

Based on model comparison and evaluation metrics, the recommended model for deployment is:

**Linear SVM with TF-IDF features**

### Justification

This model achieved:

- The **highest F1 score**
- Strong **precision and recall balance**
- Reliable detection of fake news articles

While Logistic Regression offers greater interpretability, the superior predictive performance of the Linear SVM model makes it the best overall choice for this classification task.

Therefore, **Linear SVM + TF-IDF is selected as the final deployed model.**
