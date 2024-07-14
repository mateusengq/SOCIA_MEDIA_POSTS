# SOCIA MEDIA POSTS - PREDICT IF IT IS POSITIVE, NEGATIVE OR NEUTRAL

## 1. The Project

In this project, my goal is to replicate an analysis I used to perform to evaluate NPS responses. When I received responses from clients, I labeled them as Positive, Negative, or Neutral, and then sent the Negative responses to the responsible parties to take the necessary actions.

Since I can't share the real data from my daily work, I found a dataset with some tweets and will apply the same concept to this dataset.

It's important to note that I label and send the issues to the responsible parties to enable quick actions, but I also need to read all the comments. This is just a part of the process.


 
## 2. Business Problem and Objectives
In my daily work, I collect the NPS responses, label them, analyze, calculate the NPS, and send the results to the responsible parties. Weekly, I receive a significant number of responses, and in some cases, it is necessary to take quick actions, especially with the Negative responses.

To avoid delays between receiving a response and taking action, I use a model to segment the comments. The Negative comments are sent immediately, while I read and analyze each one.

2.1. The objective here is to create a model to classify each comment.

People who work or are familiar with NPS might ask,  "Why don't you use the rating provided by clients instead of eatimate this?". In some companies in Brazil, it is common to see high ratings accompanied by improvement comments. The ideia is to identify these cases to act quickly. This classification doesn't impact the rating or the final NPS score.

2.2. Since I am using a dataset from Kaggle with a different goal, I will conduct an Exploratory Data Analysis (EDA) to better understand this dataset. My goal here is to understand the patterns in these tweets.

### 2.1. About Dataset

I used [this dataset](https://www.kaggle.com/datasets/kashishparmar02/social-media-sentiments-analysis-dataset) from Kaggle to ilustrate the ideia.
The Social Media Sentiments Analysis Dataset captures a vibrant tapestry of emotions, trends, and interactions across various social media platforms. This dataset provides a snapshot of user-generated content, encompassing text, timestamps, hashtags, countries, likes, and retweets. Each entry unveils unique stories—moments of surprise, excitement, admiration, thrill, contentment, and more—shared by individuals worldwide. [DATASET](https://www.kaggle.com/datasets/kashishparmar02/social-media-sentiments-analysis-dataset)

## 3. Pipeline:

Business problem (understanding).
Data understanding.
Data preparation.
Modelling.
Validation.


## 4. Main Insights - EDA
- The original data consists of tweets from `Instagram`, `Facebook ` and `Twitter`, with approximately 33% from each plataform.
- The original classification had 280 labels, and I decided to relabel it into just 4 labels (Positive, Negative, Other and Neutral).
    - Relabeling this information into fewer classes can help simplify the analysis and make it more manageable.
    - For the relabeling, I decided to create the groups myself, but it is important to mention that there are some libraries that analyze the data and classify it into groups, like `nltk`.
- There are 712 tweets; 401 are classified as `Positive`, 163 as `Negative`, 125 as `Other` and 43 as `Neutral`.
- After the treatments, there are 33 countries (USA, UK and Canada represent more the 50% of the texts)
- The words, considering all tweets, more common are `new`, `life`, `challeng`. For positive tweets, the words are `new`, `challeng`, and `joy`; for negative, `echo`, `despair`, `emot`; for neutral, `life`, `new`, `day` and for others, `curios`, `explor`, `nostalgia`.
- Spain is the only country that has more `Negative` tweet than `Positive`
- The correlation between Likes and Retweets is 0.99.
- There are no statistical diferences between the Sentimental and the number of Likes and Retweets.
![Boxplot_likes](https://github.com/mateusengq/SOCIA_MEDIA_POSTS/blob/main/GRAPHS/BOXPLOT_LIKES_SENTIMENT.png)
- Considering the month and Day, there are no differences between the values.
- Analyzing the hour, the hours 13:00 and 23:00 have a biggest median than the other hours.
![Boxplot_month](https://github.com/mateusengq/SOCIA_MEDIA_POSTS/blob/main/GRAPHS/boxplot_likes_month.png)



## 5. Modeling