# SOCIA MEDIA POSTS - PREDICT IF IT IS POSITIVE, NEGATIVE OR NEUTRAL

## 1. The Project

In this project, my goal is to replicate an analysis I performed to evaluate NPS responses. When I received client responses, I labeled them as `Positive`, `Negative`, or `Neutral`, and then sent the Negative responses to the responsible parties to take necessary actions.

Since I can't share the real data from my daily work, I found a dataset with tweets and will apply the same concept.

It's important to note that I label and send the issues to the responsible parties to enable quick actions, but I also need to read all the comments. This is just a part of the process.
 
## 2. Business Problem and Objectives
In my daily work, I collect the NPS responses, analyze the data, calculate the NPS, and send the results to the responsible parties. Weekly, I receive a significant number of responses, and in some cases, it is necessary to take quick actions, especially with the Negative responses.

To avoid delays between receiving a response and taking action, I use a model to segment the comments. The Negative comments are sent immediately, while I read and analyze each one.

### 2.2. Objective
The objective is to create a model to classify each comment.

People who work or are familiar with NPS might ask,  "Why don't you use the rating provided by clients instead of eatimating this?". In some companies in Brazil, it is common to see high ratings accompanied by improvement comments. The ideia is to identify these cases to act quickly. This classification doesn't impact the rating or the final NPS score.

### 2.2. About Dataset

I used [this dataset](https://www.kaggle.com/datasets/kashishparmar02/social-media-sentiments-analysis-dataset) from Kaggle to ilustrate the ideia.
The Social Media Sentiments Analysis Dataset captures a vibrant tapestry of emotions, trends, and interactions across various social media platforms. This dataset provides a snapshot of user-generated content, encompassing text, timestamps, hashtags, countries, likes, and retweets. Each entry unveils unique stories—moments of surprise, excitement, admiration, thrill, contentment, and more—shared by individuals worldwide. [DATASET](https://www.kaggle.com/datasets/kashishparmar02/social-media-sentiments-analysis-dataset)

## 3. Pipeline:

1. Business problem understanding.
2. Data understanding.
3. Data preparation.
4. Modelling.
5. Validation.


## 4. Main Insights - EDA
As this is a new dataset for me, I will do an EDA with more details to understand the dataset.

- The original data consists of tweets from `Instagram`, `Facebook `, and `Twitter`, with approximately 33% from each plataform.
- The original classification had 280 labels, and I relabeled it into just 4 labels (Positive, Negative, Other and Neutral).
    - Relabeling this information into fewer classes can help simplify the analysis and make it more manageable.
    - For the relabeling, I decided to create the groups myself, but it is important to mention that there are some libraries that analyze the data and classify it into groups, like `nltk`.
- There are 712 tweets; 401 are classified as `Positive`, 163 as `Negative`, 125 as `Other` and 43 as `Neutral`.
- After processing the data, 33 countriesare represented (USA, UK and Canada account more than 50% of the texts).
- The most common words, considering all tweets, are new, life, and challenge. For positive tweets, the words are new, challenge, and joy; for negative tweets, echo, despair, and emotion; for neutral tweets, life, new, and day; and for other tweets, curious, explore, and nostalgia.
- Spain is the only country with more `Negative` tweets than `Positive`
- The correlation between `Likes` and `Retweets` is 0.99.
- There are no statistical diferences between the `Sentimental` and the number of `Likes` and `Retweets`.
![Boxplot_likes](https://github.com/mateusengq/SOCIA_MEDIA_POSTS/blob/main/GRAPHS/BOXPLOT_LIKES_SENTIMENT.png)
- Considering the Month and Day, there are no differences between the values.
- Analyzing the hour, 13:00 and 23:00 have a higher median than the other hours.
![Boxplot_month](https://github.com/mateusengq/SOCIA_MEDIA_POSTS/blob/main/GRAPHS/boxplot_likes_month.png)

## 5. Modeling
The main objective is to estimate if the comment is `positive`, `negative`, `neutral` or `others`. Usually, the Other category is for random comments, without suggestions, or unrelated topics.

1. For the classification, I used the features Text and Hashtags, with the target being Relabeled_Sentiment. During Data Preparation, I removed punctuation, converted words to lowercase, and removed stopwords and special characters.
2. The data was split into training and testing sets with a proportion of 80:20.
3. Then, I used TF-IDF (Term Frequency Inverse Document Frequency) to transform the text into a meaningful representation for fitting machine learning algorithms.
   
$$TF - IDF = TF(t,d) x IDF(t)$$

where 
- TF: term frequency, representing the number of times term *t* appears in a document *d*
- IDF: inverse document frequency
  
$$log\frac{1 + n}{1 + df(d,t)} + 1$$

where: *n* = # of documents and *df(d,t)* is the document frequency of the term *t*.
4. I combined the features (text and hashtags) into one matrix.
5. I trained the following models
   1. Logistic Regression
   2. Logistic Regression with class weight
   3. Naive Bayes
   4. SVM
   5. SVM with class weight
   6. Random Forest
   7. Gradient Boosting
   8. Gradient Boosting with Weight


### 5.1. Results


- Best Model: Logistic Regression with Class Weight is the best performing model across all metrics, making it the preferred choice for this task.
- SVM Models: Both SVM and SVM with Class Weight are strong contenders, showing robust performance.
- Naive Bayes: A good baseline model with decent performance.
- Random Forest: Shows high precision but lower overall performance.
- Gradient Boosting: Needs careful tuning and might not handle class imbalance well without further adjustments.
- For my purpose, using comments in NPS research is helpful because the company can make quick decisions and take action.

| Model                               | Accuracy | Precision | Recall | F1 Score |
|-------------------------------------|----------|-----------|--------|----------|
| Logistic Regression                 | 0.741    | 0.826     | 0.741  | 0.712    |
| Logistic Regression with Class Weight | 0.823    | 0.853     | 0.823  | 0.809    |
| Naive Bayes                         | 0.762    | 0.826     | 0.762  | 0.731    |
| SVM                                 | 0.796    | 0.847     | 0.796  | 0.774    |
| SVM with Class Weight               | 0.796    | 0.847     | 0.796  | 0.774    |
| Random Forest                       | 0.701    | 0.847     | 0.796  | 0.774    |
| Gradient Boosting                   | 0.701    | 0.761     | 0.701  | 0.671    |
| Gradient Boosting with weight       | 0.347    | 0.514     | 0.347  | 0.295    |


![Metrics for each model](https://github.com/mateusengq/SOCIA_MEDIA_POSTS/blob/main/GRAPHS/results.png)

### 5.2. Recommendations:
- Focus on Logistic Regression with Class Weight for your final model.
- Consider further tuning SVM models for potential improvements.
- Investigate why Gradient Boosting performs poorly with class weights and explore hyperparameter tuning or alternative methods for handling imbalance.