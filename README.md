![10-news-sites-to-practice-your-English-reading-skills](https://github.com/bmjaron/capstone/assets/115658357/3ac7c034-9639-4c8e-a663-8d2f3b287608)

# Predicting Political Articles

**Author**: [Benjamin Jaron](mailto:bmjaron@gmail.com)

# Table of Contents
* [Repository Structure](#I.Structure)
* [Overview](#II.Overview)
* [Data and EDA](#III.EDA)
* [Text Cleaning](#IV.Cleaning)
* [Modeling](#V.Modeling)
* [Conclusions](#VI.Conclusions)

# I. Repository Structure

Aside from this README file, our repository contains a Jupyter notebook, a .gitignore file, and a [slide deck](https://github.com/bmjaron/capstone/blob/main/slide_deck.pdf). Our repository **does not** contain a data file. It is very large and did not fit, and in order to ensure reproducability our notebook contains instructions of how to upload it thru Kaggle.

# II. Project Summary

We are attempting to help those who read political articles professionaly develop a model to discard unrelated content and pin down political articles. This will in turn help them save a tremendous amount of reading time.

Our project begins by importing a data set from Kaggle ([linked here](https://www.kaggle.com/datasets/rmisra/news-category-dataset)) which contains about 210,000 news articles. We use the NLTK tools in order to help us vectorize the data and prepare for modeling.

We then undertake an iterative modeling process and test for f-1 score. Our final model returns a f-1 score of 0.60, but does incredibly well at discarding non-political articles with a precision score of 0.94.

Our final recommendation is to use our model in order to discard unrelated content and then rely on the human reader to sift thru the remaining articles and find those related to politics. Once our model takes care of most of the dirty work, this shouldn't be such an overwhelming task.

# II. Business Problem

Despite living in a world with convenient online access to information and news, [this](https://www.nngroup.com/articles/how-people-read-online/) report from the Nielsen Norman Group has shown the most readers do not read online. This is because humans still prefer articles that conform with their personal preferences, and find searching for and reading articles online to be a waste of time. A [second](https://www.orientation.agency/insights/how-people-read-online) report from Orientation shows similar findings, and highlights that users only spending about 15 seconds on a given web page before moving on.

As a result of this predicament, there is a need to build technology to hand-pick online articles to provide readers with the content they need without wasting time.

Our target clientele are those who work in the politics, lobbyists, think tank employees, or any other individual that must read political articles for their work. In contrast to those who skim the news in their spare time, these individuals must be current with political news in order to properly perform their jobs. As such, it is necessary for them to be able to identify political articles and discard unrelated and distracting content.

Our goal is to build a model that can predict a political article given a short description of that model. This will in turn provide our cleints with the ability to pin-down their required reading with efficiency.

# III. Data and EDA

Our [data set](https://www.kaggle.com/datasets/rmisra/news-category-dataset) contains 209,527 news articles from the Huffington Post. Each entry is a different article containing a link, headline, category, short description, authors and date. There are 42 distinct categories of articles.

![pic_1](https://github.com/bmjaron/capstone/assets/115658357/d0c4f63e-3488-4e3e-a034-b25750b122d0)
![pic_2](https://github.com/bmjaron/capstone/assets/115658357/3de44006-a34d-4b0b-8b96-ce4d2d6d3940)

From the above visuals we can see that we have imbalance across the categories. This is amplified as we convert categories for a 2-class classification problem. This is accounted for using imbalance learn to randomly undersample.

![pic_3](https://github.com/bmjaron/capstone/assets/115658357/8a626f9b-fb52-49b0-92e7-674135b161c1)

# IV. Text Cleaning

In order to properly process our articles, we used a relatively conventional cleaning and tokenization process using NLTK's built-in functions. We first strip all text of special characters and punctuation using regular expression. We then used NLTK's tokenizer. We also stemmed and lemmatized, and removed all English stopwords.

# V. Modeling

## A. Overview (and a word about our scoring metric)

The model that we used was a logistic regression classifier, and we were able to achieve a f-1 score of 0.60. We also had precision of 94& with the negative class.

We felt that f-1 score, which is a score the measures the balance of maximizing rate of predicted positives while minimizing false positives, was the most approriate method to score our model. Our business problem is to deliver a model that helps readers isolate political articles. As a result we want as many true political articles as possible, while limiting falsely predicted political articles. 

## B. Validation method and vectorization

In order to validate our model, we divided the data into 3 sets: training, testing and a holdout. The models were trained on the training set, and each iteration was tested on the testing set. We ran the final model on the unseen holdout set.

An important element of our modeling process was converting our text data into features for modeling. We utilized the TF-IDF vectorizer.

# VI. Final Model and Recommendation

While our target metric of F-1 score is 0.60 and is not particularly astounding, our model still does provide real value. Although we might not be able to predict political articles with perfection, our model is incredibly effective at correctly identifying non-political articles. The precision score of predicting the non-politics class is 0.94! This makes sense given the imbalance of the set; a model ran on a set with many negatives will tend to predict negatives correctly.

Below we show the confusion matrix of our final model.

![download (1)](https://github.com/bmjaron/capstone/assets/115658357/58a8fab8-a3d6-4d08-9976-21a8114255b9)


Based on our results, our recommendation to the stakeholder is the following. Use our model in order to help weed out the vast majority of non-political articles. Once that has been accomplished, the reader will have a much easier time using his human eyes to select the political articles from the non-political articles. This conforms with the findings we found in the Nielsen Norman Group [report](https://www.nngroup.com/articles/how-people-read-online/) that the human reader filters unrelated content according to his preferences. Although readers still prefer non-digital platforms to read news, our model provides an opening to discad the bulk of unrelated content and gives the reader a less overwhelming online experience.

We understand that this project is only a cursory exploration of this particular problem. Time constraints and computational limitations meant that we couldn't exhaust model options for this large set. There is more room to explore whether or not a higher f-1 score can be obtained. Additionally, another point of exploration is attempting a multi-class classification problem.

