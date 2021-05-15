## Executive Summary

As an audio news aggregator mobile APP, Newsly reads the latest trending web articles to users in a natural human voice. It has a great interface where users can view the top trending articles of the day on the home page, select news articles by country and choose articles by category. In addition to the variety of functions Newsly has, we believe a recommendation system could make the APP more attractive to users. In this proposal, we plan to apply two methods on Newsly’s data set to make recommendations to users on audio articles they might be interested in. The first method is the general approach, which recommends based on popularity of previous user listening history. This approach is more suitable for new users that have not clicked on any articles yet. The other method is the article specific approach, which recommends based on related topics. Since we do not have a large amount of data, there exist some limitations to both approaches. Further development may involve actions like eliminating noise factors (test users) from the data set, and making more personalized recommendations with data that link users and articles together.

## Introduction

Nowadays, there are hundreds of news articles generated and posted hourly. With a massive amount of information, it is hard for users to quickly find what they are interested in{cite}`recommendation`. A recommendation system helps with this problem. In this capstone, we propose to develop two methods that make recommendations to users that could improve user experience and increase user engagement.

- General Recommendation: Provide generic recommendations based on the news articles that are most popular among users on the application. 
- Article-Specific Recommendation: Using a specific news article to make recommendations based on the related topics.

We would like to have our code in Python files as our end product and deploy it to cloud (either AWS or Canarie) for Newsly to run on their own.

### *EDA*

Newsly uses both AWS and Google Analytics to store their data. Data in AWS are mainly information about users and news articles while data in Google Analytics are events and activity counts. After going through all the data on both platforms, we find three tables useful. The first one is the `listened article` shown in table 1. It contains the title of the article that existing users have clicked on and the total number of clicks. This information helps us to define the popular topics existing users were interested in.



## Data Science Techniques

### *General Recommendation:*

General recommendation implies non-user-specific recommendation, which means the same content will be recommended to all the users, and the recommendation is not personalized. This method is expected to be mainly applied for new users. Because if the user’s browsing history and listening preference are unknown, the app should simply provide recommendations of popular articles.

Determining whether an article is popular is straightforward if it has already been published for at least one day, since the number of views/listens can be observed. However, if an article is newly published, the system will have to predict the popularity of that article.

The core idea in popularity prediction is determining whether an article belongs to a popular topic. For example, from the past records, the system found that COVID-19 has been a very popular topic in the past few days. If a newly published article is also about COVID-19, then the system should be recommending this new article. To achieve this, a variety of machine learning techniques, especially natural language processing techniques would be applied.

There are two main processes for this approach, process A is classifying the historical articles by different topics, process B involves making popularity predictions based on the result from process A, below are the detailed descriptions.

Figure 1 represent the two main process of the general recommendation approach.

```{figure} images/general.png
---
height: 400px
name: geneal_approach
---
Illustration of general recommendation approach
```

### *Article-specific recommendations:*

The general recommendation approach described in the previous section would be advantageous when a new user uses the Newsly application for the very first time. Articles would be recommended to the user based on popularity among other listeners. However, this approach is limited since it cannot provide personalized recommendations to each and every user based on the articles that they decide to listen to. This is where the article-specific recommendations come in.

An article-specific recommendation refers to an article that may be related to another article that the user has clicked on. For example, suppose a user clicks on an article titled “Canada to get two million Pfizer vaccine doses”. An example of a related article that could be recommended to the user could be: “80% of Canadians support COVID-19 vaccine passports for travel: poll”. This is what we aim to do with article-specific recommendations.

Our main idea is to build a system that can identify which articles that are currently present on the Newsly application are related to each other. Once these relations between articles have been established, recommendations can be made for a user in real-time i.e. when an article is clicked.

There are 2 main processes that are a part of this approach that we have labelled process A and B. The high level view of these are shown below in Figure 1 and Figure 2:

```{figure} images/input_output.png
---
height: 400px
name: input_1
---
Process A: Create Index of articles in Trends table
```
```{figure} images/input_output_2.png
---
height: 400px
name: input_2
---
Process B: Recommend top 'N' articles related to what the user clicked
```

Below is the detailed description of both processes:

1. **Process A:** This process is responsible for creating an index of all articles that are currently in the Trends table which will help in knowing which articles are related to each other, and will be used by process B to make recommendations for the user.

The process is triggered when either of the following events occur:
- A new article is added to the Trends table or
- An article is deleted from the Trends table

<u>Process Steps</u>: The steps of this process have been described in Fig 3

```{figure} images/Process_A.png
---
height: 400px
name: process_A
---
Process A
```

<u>Dependency</u>: This process depends on information from the Trends table

<u>Process output</u>: An index of articles and relationships that will be used to recommend articles that are related to the one clicked by the user.

2. **Process B:** This process recommends the top N articles related to the one that the user has just clicked on. To find related articles, the process would use the index created by Process A.

This process would be triggered when a user clicks on any article in the Newsly application.

<u>Process Steps</u>: The steps of this process have been described in Figure 4

```{figure} images/Process_B.png
---
height: 400px
name: process_B
---
Process B
```

<u>Dependency</u>: The URL of the article clicked by the user needs to be passed to the recommender system.

<u>Process output</u>: Top N recommendations related to the article clicked by the user

## Project Timeline

This project will have 3 broad phases: Ideation and Brainstorming, Development of the recommendation system and final submission of data product and report. These broad phases have been broken down and explained further in the Figure 5.

```{figure} images/Timeline.png
---
height: 400px
name: Timeline
---
Capstone timeline
```

## Bibliography

```{bibliography} references.bib
```
