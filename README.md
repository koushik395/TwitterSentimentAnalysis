# TwitterSentimentAnalysis
What is sentiment analysis? Sentiment Analysis is the process of ‘computationally’ determining whether a piece of writing is positive, negative or neutral. It’s also known as opinion mining, deriving the opinion or attitude of a speaker. Why sentiment analysis?

1. Business: In marketing field companies use it to develop their strategies, to understand customers’ feelings towards products or brand, how people respond to their campaigns or product launches and why consumers don’t buy some products.
1. Politics: In political field, it is used to keep track of political view, to detect consistency and inconsistency between statements and actions at the government level. It can be used to predict election results as well!
1. Public Actions: Sentiment analysis also is used to monitor and analyse social phenomena, for the spotting of potentially dangerous situations and determining the general mood of the blogosphere.

**Here,I am going to use “Tweepy,” which is an easy-to-use Python library for accessing the Twitter API. You need to have a Twitter developer account and sample codes to do this analysis. You can find the Colab Notebook code in my Github Repository.**

## What is Text Blob
TextBlob is actually a high level library built over top of NLTK library. First we call clean_tweet method to remove links, special characters, etc. from the tweet using some simple regex. Then, as we pass tweet to create a TextBlob object, following processing is done over text by textblob library:
* Tokenize the tweet ,i.e split words from body of text.
* Remove stopwords from the tokens.(stopwords are the commonly used words which are irrelevant in text analysis like I, am, you, are, etc.)
* Do POS( part of speech) tagging of the tokens and select only significant features/tokens like adjectives, adverbs, etc.
* Pass the tokens to a sentiment classifier which classifies the tweet sentiment as positive, negative or neutral by assigning it a polarity between -1.0 to 1.0 .
* TextBlob uses a Movies Reviews dataset in which reviews have already been labelled as positive or negative.
* Positive and negative features are extracted from each positive and negative review respectively.
* Training data now consists of labelled positive and negative features. This data is trained on a Naive Bayes Classifier.
* Finally, parsed tweets are returned. Then, we can do various type of statistical analysis on the tweets. For example, in above program, we tried to find the percentage of positive, negative and neutral tweets about a query.


## Step 1: Install and Import Libraries
Before analysis, you need to install textblob and tweepy libraries using !pip install command on your Colab Notebook.

### Install Libraries
!pip install textblob <br>
!pip install tweepy


You need to import libraries that you will use in this sentiment analysis project.

import re
import tweepy as tw
from textblob import TextBlob
import pandas as pd
import nltk
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
import matplotlib.pyplot as plt



## Step 2: Authentication for Twitter API
Before the authentication, you need to have Twitter Developer Account. If you don’t have, you can apply by using this [https://developer.twitter.com/en](link). Getting Twitter developer account usually takes a day or two, or sometimes more, for your application to be reviewed by Twitter.

Open the above mentoned link and click the button: 'Developer Portal'<br>
1.Fill the application details.<br>
2.Once the app is created, you will be redirected to the app page.<br>
3.Open the ‘Keys and Access Tokens’ tab.<br>
4.Copy ‘Consumer Key’, ‘Consumer Secret’, ‘Access token’ and ‘Access Token Secret’.

### Authentication
1. consumerKey = “Type your consumer key here”
1. consumerSecret = “Type your consumer secret here”
1. accessToken = “Type your accedd token here”
1. accessTokenSecret = “Type your access token secret here”
1. auth = tweepy.OAuthHandler(consumerKey, consumerSecret)
1. auth.set_access_token(accessToken, accessTokenSecret)
1. api = tweepy.API(auth)


After your authentication, you need to use tweepy to get text and use Textblob to calculate positive, negative, neutral, polarity and compound parameters from the text.

## Step 3: Fetching Tweets
#### tw.cursor 
We use pagination a lot in Twitter API development. Iterating through timelines, user lists, direct messages, etc. In order to perform pagination we must supply a page/cursor parameter with each of our requests. The problem here is this requires a lot of boiler plate code just to manage the pagination loop. To help make pagination easier and require less code Tweepy has the Cursor object.

To know more about tweepy visit [https://docs.tweepy.org/en/v3.5.0/api.html]

## Step 4: Cleaning Tweets to Analyse Sentiment
Firstly, I create new data frame (tw_list) and a new feature(text), then clean text by using lambda function and clean RT, link, punctuation characters and finally convert to lowercase.
Use regualr expression to clean RT, link, punctuation characters etc.. and finally convert to lowercase and then split the sentence into tokens.
Now using for loop check whether those tokens are present in stopwords are not.If not then add those tokens to empty list.Then join all those tokens to get a sentence.

## Step 5: Sentiment Analyse
Now, I can use cleaned text to calculate polarity, subjectivity, sentiment, negative, positive, neutral and compound parameters again. For all calculated parameters, I create new features to my data frame.When you have a look tweet list you can see some duplicated tweets, so you need to drop duplicate tweets.
