# Airline Review Sentiment Analysis (VADER, TextBlob, Transformer)

**Student:** Marcela Lozano  
**Project Type:** Assignment 1 Sentiment Analysis 

## Overview
This project is an analysis of British Airlines customer reviews using three sentiment analysis approaches:
- Vader (A lexicon based sentiment compound score)
- TextBlob (Polarity based sentiment)
- transformer (Emotion Based Deep Learning Model)

The goal is to compare model performance against manually labeled ground truth reviews. The project begins with Exploratory Data Analysis and includes visualizations and commentary on variable correlations, review length, etc. 


## Requirements


### Python Libraries

-  pandas 
-  numpy 
-  matplotlib
-  seaborn
-  scikit-learn 
-  nltk
-  textblob
-  wordcloud
-  transformers
-  torch

# Dataset

The dataset consists of airline customer reviews with:
- Review text
- Overall ratings (1–10)
- Service feature ratings (SeatComfort, CabinStaffService, etc.)


### Key Columns Used
- `vader_text` → Text input for VADER
- `textblob_text` → Text input for TextBlob
- `transformertext` → Text input for Transformer
- `ground_truth` → Manual sentiment labels
## First-Time Setup (NLTK Downloads)

Run once before executing the main code:

``` python
import nltk
nltk.download("vader_lexicon")
nltk.download("punkt")
nltk.download("stopwords")
```

## Sentiment Labeling Methodology

### VADER

-   Labeling using compound sentiment score
-   Thresholds:
    -   Positive: ≥ 0.05
    -   Negative: ≤ -0.05
    -   Neutral: otherwise

### TextBlob

-   Labeling using polarity score
-   Thresholds:
    -   Positive: ≥ 0.10
    -   Negative: ≤ -0.10
    -   Neutral: otherwise

### Transformer

-   Uses HuggingFace emotion classifier
-   Emotion labels are mapped to sentiment:
    -   Positive: joy, love
    -   Negative: anger, sadness, fear
    -   Neutral: surprise (documented design choice)

## Accuracy Evaluation

The accuracy was computed against manually labeled ground truth:

``` python
from sklearn.metrics import accuracy_score

vader_acc = accuracy_score(sample_100["ground_truth"], sample_100["vader_pred"])
textblob_acc = accuracy_score(sample_100["ground_truth"], sample_100["textblob_pred"])
transformer_acc = accuracy_score(sample_100["ground_truth"], sample_100["transformer_pred"])
```

## Expected Outputs

-   EDA visualizations (heatmaps, word clouds, histograms)
-   Sentiment prediction columns:
    -   vader_pred
    -   textblob_pred
    -   transformer_pred
-   Model accuracy comparison table
-   Interpretation heatmaps for model analysis

#Sampling Approach
A random sample of 100 airline reviews were selected from the full dataset to allow for manual ground truth labeling. The ground truth labels were set to test model performance and a fixed random seed was used to ensure reproducibility across models.
This was how we accounted for a fair and controlled comparison.

# Model Accuracy Results

- **Transformer:** 69%
- **VADER:** 58%
- **TextBlob:** 35%

The Transformer model had the highest performance showing a stronger understanding of text context for long and nuanced airline reviews. VADER didn't have the worst performance but specifically struggled with the detection of netural reviews. TexBlob had the weakest performance and this is likely due to the high reliance on a simple polarity score without contextual understanding.

Overall, the deep learning models perform better than the lexicon based models for analyzing complex customer reviews.

# Key Findings

## 1. Model Performance Comparison
The Transformer model achieved the highest accuracy compared to lexicon-based methods confirming that context-aware deep learning models better capture nuanced sentiment in long airline reviews.

- Transformer: Highest accuracy (context-aware)
- VADER: Moderate accuracy (good with strong emotional language)
- TextBlob: Lowest accuracy (struggles with nuanced reviews)

This aligns with expectations since airline reviews often contain mixed sentiment and long explanations.

---

## 2. Sentiment Behavior in Airline Reviews
The analysis revealed that:
- Negative reviews tend to be significantly longer than positive reviews
- Customers with low ratings (1–3) provide more detailed complaints
- High ratings (8–10) are shorter and more direct

This suggests dissatisfied customers are more expressive and descriptive.

---

## 3. Correlation Insights from EDA
The correlation heatmap showed strong positive relationships between overall rating and service related features like Value for Money, Cabin Staff Service, and Inflight Entertainment.


---

## 4. Model Strengths and Weaknesses

### VADER
Strengths:
- Performs well on clearly emotional language
- Fast and interpretable

Weaknesses:
- Struggles with neutral or mixed reviews
- Limited contextual understanding

### TextBlob
Strengths:
- Simple polarity scoring
- Overall quick

Weaknesses:
- Overly sensitive to individual word polarity
- Poor handling of long narrative reviews

### Transformer Model
Strengths:
- Context aware sentiment understanding
- Best performance on nuanced airline complaints

Weaknesses:
- Computationally slower


---


## Important Notes

-   Stopwords are removed only for EDA and word clouds but not for the text used in
    sentiment models
-   Do NOT reload sample_100 after creating prediction columns
-   Always run prediction cells before computing accuracy
-   Use truncation=True for transformer instead of character slicing
-   Data was cleaned differently for each model according to respective requirements
-   It is expected for the transformer to run slowly due to deep learning inference.