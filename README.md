This project of ours is based on the article:
# TClustVID: A novel machine learning classification model to investigate topics and sentiment in COVID-19 tweets
> [DOI: 10.1016/j.knosys.2021.107126](https://doi.org/10.1016/j.knosys.2021.107126)

## 📊 Data: The COVID-19 Twitter  
The data used in this project is derived from the model **Long Short-Term Memory (LSTM)**.  

- **📌 Source:** [IEEE Data Portal](https://ieee-dataport.org/)  
- **✍️ Author:** Rabindra Lamsal  

### 📝 Data description  
- **clean_tweet:** Tweets cleaned from original data.  
- **class:** Classification labels with values:  
  - `0` → Negative  
  - `1` → Neutral  
  - `2` → Positive

## 🛠 Preprocessing  

### 🔍 Handling missing data
- **Find missing data rate:** ~0.003% → removing missing data lines will not affect the model.  

### 🏗 Tokenization includes 3 processes:  
1. **Stemming processing:**  
   - The process of truncating and transforming words in a text back to their original form, usually by removing suffixes.  
   - Using **Snowball stemmer** has higher accuracy than **Porter stemmer**.  

2. **Lemmatizing processing:**  
   - The process of transforming words in a text back to their original form (using **Wordnet lemmatizer**).  
   - Review the lexical and grammatical structure of the word to ensure that the word is converted to the correct form.  

3. **Tokenizing processing:**  
   - For each original tweet, it will be performed in turn from: **Stemming → Lemmatizing → Tokenizing**.  
   - The final data will be saved in the variable `document_word`.  

### 📖 Create dictionary  
- Create dictionary for words appearing in the original data file based on 'document_word'. 

### 🎯 Filter dictionary  
- Remove words that **appear in tweets less than 15 times**.  
- Remove words with a **common occurrence rate of less than 10%**.
- Keep a maximum of 100000 words → remove noisy data in prediction 

### 🏗 Create Bag_of_word: 
- Create bow using dictionary of original data  

## 🔍 Clustering  

### 🏗 Data Vectorization  
- The initial dataset is **vectorized** using the `doc2id` method based on the dictionary.  
- **Padding** is applied to standardize the dimensions of the vectors.  

### 📊 K-Means Clustering  
- The **K-Means** clustering algorithm is employed with **k = 5** to cluster the **vectorized and padded data**.  
- For each cluster `(0, 1, 2, 3, 4)`:  
  - The **proportion of data** belonging to the cluster is evaluated.  
  - The cluster's **performance** is assessed using:  
    - **Accuracy**  
    - **Area Under the Curve (AUC)**  
    - **F-measure**  
    - **G-mean**  
    - **Sensitivity**  
    - **Specificity**  

### 🏷 Data Classification Based on Clustering  
- The **highest-performing cluster** is identified within the **vectorized and padded dataset**.  
- Data is then categorized into **three subsets** based on the `class` values:  
  - `0` → **Negative**  
  - `1` → **Neutral**  
  - `2` → **Positive**  

### 📖 Class-Specific Bag of Words Extraction  
- From the **three classified datasets**, a **Bag of Words (BoW)** is extracted using the original dataset's `bag_of_word`.  
- This results in three **class-specific BoWs**:  
  - `bow_neg` → Negative class  
  - `bow_neu` → Neutral class  
  - `bow_pos` → Positive class  

## 🔥 Latent Dirichlet Allocation (LDA)  

### 🏗 Topic Modeling with LDA  
Using the **Latent Dirichlet Allocation (LDA)** model, topic distributions are extracted for the three **sentiment-based Bag of Words (BoW)** datasets:  
- `bow_neg` → Negative sentiment  
- `bow_neu` → Neutral sentiment  
- `bow_pos` → Positive sentiment  

### 🔍 LDA Assumptions  
- LDA assumes that each tweet in a **large dataset** is generated through a **hidden generative process**.  
- Each tweet is considered a **mixture of multiple topics**, while each topic itself is a **distribution over words** based on **probabilistic modeling**.  

### 📊 LDA Output  
- The **final result** consists of:  
  - A set of **topics** corresponding to each sentiment class.  
  - A **probability distribution** of words associated with each topic.  

