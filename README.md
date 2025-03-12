# NOT A RELIABLE PROJECT WITH DISCREPENCIES ON LANGUAGE TRANSLATION

# DS_WEBSCRAPING_SENTIMENT_ANALYSIS
Web Scraping tweet(X) data for Sentiment Analysis

# END-TO-END WEBSCRAPING AND SENTIMENT ANALYSIS

**PROJECT DESCRIPTION:**
-----------------------------------------------------------
- This project analyzes public sentiment on Petronas recent rightsizing by extracting and classifying tweets. 

- Integrates `VADER`, a rule-based sentiment analysis tool, with a `Machine Learning (ML) classifier using (TF-IDF + Logistic Regression)` features. 

- The goal is to improve sentiment classification accuracy by combining these two approaches.

- The dataset consists of 130+ tweets collected from December2024 until now. Each tweet is classified into Positive, Neutral, or Negative sentiment. 

**PROJECT ARCHITECTURE:**
-----------------------------------------------------------

        ┌──────────────────────────────┐  
        │  **TWITTER SCRAPING**        │  
        │  Playwright (Headless)       |
        │  Chromium                    |
        │  Anti-bot detection bypass   │  
        └───────────────┬──────────────┘    
                        ▼  
        ┌──────────────────────────────┐  
        │   **DATA PREPROCESSING**     │  
        │  Cleaning & Formatting       │  
        └───────────────┬──────────────┘   
                        ▼  
        ┌──────────────────────────────┐  
        │  **RAW DATA STORAGE (LOCAL)**│  
        │  Backup before processing    │  
        └───────────────┬──────────────┘  
                        ▼  
        ┌──────────────────────────────┐  
        │  **SENTIMENT ANALYSIS**      │  
        │  VADER (Lexicon-based)       │  
        │  ML Model (TF-IDF + LR)      │  
        └───────────────┬──────────────┘  
                        ▼  
        ┌──────────────────────────────┐  
        │  **SENTIMENT CONSOLIDATION** │  
        │  VADER + ML Decision Logic   │  
        └───────────────┬──────────────┘  
                        ▼  
        ┌──────────────────────────────┐  
        │  **DATA EXPORT & REPORTING** │  
        │  Excel / CSV                 │  
        │  Sentiment Charts            │  
        │  ML Model Evaluation         │  
        └──────────────────────────────┘  



# PROJECT FLOW:
-----------------------------------------------------------

## 1. DATA COLLECTION
### WHY?
- `Twitter` is a major platform for real-time reactions to events.
- Easy to get latest sentiment on the recent Petronas rightsizing topic.
- Data is saved in CSV and Excel formats for further processing.

### HOW?
- `Playwright` is used to automate tweet scraping.
- keyword is define such as `Petronas layoff`, `Petronas Rightsizing`, and etc.
- Ensured data quality by:
  - Removing duplicates.
  - Limiting tweets to December 2024 onwards.
  - Extracting only text, usernames, and timestamps.

### KEY DETAILS
- Opened Twitter’s live search with `Playwright` and it will open `chromium`
- Need to login manually to avoid authentication blocks.
- Extracted up to 500 tweets per keyword But if there is only 15 tweets based on keyword, it will take 15.
- Used random sleep intervals (15s to 45s) to mimic real user behavior.
- Stored data as tweets_v5.csv and tweets_v5.xlsx and etc.

## 2. DATA PREPROCESSING
### WHY?
- Raw tweets contain unnecessary elements such as links, spaces, and formatting inconsistencies.
- Proper cleanup improves the accuracy of sentiment analysis.

### HOW?
- Converted timestamps to datetime format.
  - 20240306 14:30:15 ----> 2024-03-06 14:30:15
- Removed URLs.
- Stripped excess spaces.
- Ensured data types were correctly formatted before analysis.

![Screenshot 2025-03-11 at 2 19 56 PM](https://github.com/user-attachments/assets/5ee55f64-2af6-4664-b93d-3151bd7c7d06) 


## 3. SENTIMENT ANALYSIS (VADER + ML)
### WHY?
- `VADER (Valence Aware Dictionary and sEntiment Reasoner)` = good for short social media text
  - But it might misinterpret sarcasm and specific language
- `TF-IDF + Logistic Regression` = helps classify sentiment based on patterns learned from labeled data.
- Combining `(VADER + ML)` approaches ensures a more accurate and robust sentiment classification.

### HOW?
- `VADER Sentiment Analysis`
  - Every tweet receive score from `VADER`
    - Score ≥ 0.05 → Positive (🙂)
    - Score ≤ -0.05 → Negative (😞)
    - Otherwise → Neutral (😐)

- `Machine Learning Model ML (TF-IDF + Logistic Regression)`
  - `TF-IDF Vectorizer` (max_features=5000) extracts important words from tweets.
  - Split data into 80% training, 20% testing.
  - Trained a `Logistic Regression Model` (max_iter=1000) for classification.
  - Labeled outputs as:
    - 1 → Positive 🙂
    - -1 → Negative 😞
    - 0 → Neutral 😐

## 4. FINAL SENTIMENT CONSOLIDATION
### WHY?
- To resolve conflicting predictions between `VADER and the ML model`.
- ML models typically perform better in structured classification tasks.

### HOW?
- If both methods agree on sentiment → Keep it.
- If disagree → Prioritize ML prediction as it is trained on labeled data.
- Example:

![image](https://github.com/user-attachments/assets/29d4f820-9f12-4840-b2a1-723b04081786)

## 5. VISUALIZATION
- Used `Seaborn` and `Matplotlib` to generate a bar chart of sentiment distribution.
- Based on the result 41% the model needs more round of trying and a better and more set of tweets.
- 41% is on the low area and the model struggle to classify the tweets.
- Probably a better cleanup, increasing the volume to 500 or more.

## FINAL THOUGTHS (ARTIFICIAL INTELLIGENCE)
Your sentiment model needs more refinement, especially for negative and positive sentiment detection. 
## SUGGESTION (ARTIFICIAL INTELLIGENCE)
- Reduce the number of Neutral tweets to match the smaller classes:
- Oversample Positive & Negative `(SMOTE)`
- Improve Features `(TF-IDF Adjustments)`
- Retrain the Model with the Balanced Data

![image](https://github.com/user-attachments/assets/ea1c6bc3-2740-46b5-b890-13d7ca10199e)

 
