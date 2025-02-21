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

### 🔍 Xử lý dữ liệu thiếu  
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



