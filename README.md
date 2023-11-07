# Sentiment_analysis
Sentiment analysis on [Amazon food review](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews) using Vader, Bert, and Roberta.

Also talked about the pros and cons of each approches briefly.

## Data overivew
<img width="493" alt="Screenshot 2023-11-07 at 00 48 22" src="https://github.com/tianw52/sentiment_analysis/assets/129543727/aa8bef7a-7093-478b-ab72-955215cadf8d">


The dataset has 50,000+ rows with 10 different features, in the project we mainly used "Score" which is the review stars, and "Text" which is the actual review.

<img width="822" alt="Screenshot 2023-11-07 at 00 48 57" src="https://github.com/tianw52/sentiment_analysis/assets/129543727/fb6e15f0-09db-495b-a09c-0143329580c6">

Notice that the reviews are unbalanced, most of the reivews are highly positive.

** NOTE: for the purpose of this project, we use the stars are references to verify the accuracy of our models.**

## 1. Vader
Firstly, we use Vader, which is a bag-of-n-garms approach.

### Sample Result
<img width="822" alt="Screenshot 2023-11-07 at 00 52 45" src="https://github.com/tianw52/sentiment_analysis/assets/129543727/27094dd1-e4cd-41b3-9c8b-8bb686487247">

### Results Visualization

<img width="1015" alt="Screenshot 2023-11-07 at 00 52 58" src="https://github.com/tianw52/sentiment_analysis/assets/129543727/4ac0464c-6179-4da9-8020-13d1b5ca4591">

### Drawback
<img width="1013" alt="Screenshot 2023-11-07 at 00 53 13" src="https://github.com/tianw52/sentiment_analysis/assets/129543727/41e5f4a3-5095-447d-a65d-e3a63398b652">

In the above example we see that the result is not accurate at all. This is because the Vader model use bag of n-grams approach, i.e. it take tokens individually without considering the sequence/order, which is important in human languages, for sentiment analysis

** For Berta and Roberta, we only use the first 1000 rows of the dataset**

## 2. Bert
Secondly, we use Bert which is a **bidirectional** transformer pretrained using a combination of masked language modeling objective and next sentence prediction on a large corpus comprising the Toronto Book Corpus and Wikipedia.

### Sample Result

To verify our result, we compare the model output ('sentiment score') with the user input review stars ('Score'). 
<img width="765" alt="Screenshot 2023-11-07 at 01 48 40" src="https://github.com/tianw52/sentiment_analysis/assets/129543727/9545bcd5-51e5-43be-8fc1-0e4f3db72b7b">

We defined aligned to be 1 if the model output is within +- 1 of the user input stars.

<img width="865" alt="Screenshot 2023-11-07 at 01 53 25" src="https://github.com/tianw52/sentiment_analysis/assets/129543727/d9e43107-747f-4de5-82fd-6e09925b2b04">

<img width="437" alt="Screenshot 2023-11-07 at 01 56 54" src="https://github.com/tianw52/sentiment_analysis/assets/129543727/e6e3b4fa-d08f-4e03-aaeb-27a2d84d5556"> 

The accuracy is about 92.43%.

## 3. Roberta

Lastly, we use Roberta which builds on BERT and modifies key hyperparameters, removing the next-sentence pretraining objective and training with much larger mini-batches and learning rates.

### Sample Result
<img width="918" alt="Screenshot 2023-11-07 at 02 03 04" src="https://github.com/tianw52/sentiment_analysis/assets/129543727/7fc6cb91-a24c-42dd-a955-7f70bd2c703a">

### Results Visualization
<img width="1013" alt="Screenshot 2023-11-07 at 00 54 03" src="https://github.com/tianw52/sentiment_analysis/assets/129543727/634a7c32-6bb6-4683-8400-3ea5e1d03f72">

Like Vader, the positive and negative sentiment scores behave like what we expected (the more the stars, the more positive the reviews). However, unlike how the neutral sentiments score are evenly distributed in Vader, Roberta has a normal distribution, which make sense because 3 out of 5 means a netural rating and the more extreme the stars, the less netural the rating.
