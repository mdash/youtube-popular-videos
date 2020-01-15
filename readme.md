# Analysis of trending videos on Youtube India

Analysis of trending videos data from Youtube. Please check out the [blog post](https://medium.com/@md047/what-are-the-types-of-videos-that-trend-on-youtube-cadcebf51115). 

## Objective

The objective is to tease out relationships within trending YouTube videos in India based on the available data.

## Approach

Broadly the following approach was adopted:

    - EDAs with distributions of the various features
    - Modeling the # views that trending videos get against the features
    - SHAP and PDP plots to quantify the impact of the features against the # views that a video gets

CRISP-DM Framework was used to answer the following questions:

    1. What are the categories of trending videos?    
        - Business Understanding: The category of videos represent the genre of the video and is an essential classification that when explored gives an idea of what youtube users in India are generally interested in. 
        - Data Understanding: For answering this question, the entire dataset of trending videos from the 2017-18 timeframe was used and the # of occurences of each category of video in the trending list was evaluated.
        - Descriptive Analysis: Barplots were used to evaluate the # videos in a category that show up in the trending list of videos in the timeframe of the data.

    2. What is the general sentiment towards trending videos?
        - Business Understanding
        - Data Understanding
        - Prepare Data
        - Descriptive Analysis
    3. Does my old video still have a chance of trending?
        - Business Understanding
        - Data Understanding
        - Prepare Data
        - Descriptive Analysis
    4. When are the most popular videos published?
        - Business Understanding
        - Data Understanding
        - Prepare Data
        - Descriptive Analysis
    5. What are the most frequent tags attributed to trending videos?
        - Business Understanding
        - Data Understanding
        - Prepare Data
        - Descriptive Analysis
    6. Which of these factors is more important?
        - Business Understanding
        - Data Understanding
        - Prepare Data
        - Data Modeling
        - Evaluate the Results


## Packages used

The following is a list of packages used for the analysis:

    pandas
    numpy
    pickle
    matplotlib
    seaborn
    pandas_profiling
    json
    tqdm
    sklearn
    wordcloud
    autoviz
    calendar
    lightgbm
    shap
    pdpbox

## Motivation

With increasing badwidths, and cheaper cost of on-the-go cellular bandwidth in India, video consumption has gone up exponentially. In this scenario, it is a very interesting prospect to have a good understanding of what consumers like in their media. The motivation for this project was to understand something about the videos that trend and are popular on youtube. 

## Datasets and files

Files in the repository:

1. ```YouTube India Trending Videos.ipynb``` - IPython notebook fine with analysis steps and code
2. ```experiment1_resuts.csv``` - Dump of GridSearchCV run. Can be ignored.

Datasets:

1. Trending videos data sourced from Kaggle - [link](https://www.kaggle.com/datasnaek/youtube-new). Files:
    - ```./data/IN_category_id.json```
    - ```./data/INvideos.csv```

2. India holidays data sourced from https://www.timeanddate.com/holidays/india
    - ```./data_pull/holidays_india_17_18.csv```

## Summary of results

A quick summary of the results:

    - Videos in entertainment, music, comedy and news are among the trending categories
    - However, gaming, movies and sports score high on average views per video
    - Comedy and Education videos have the most positive sentiment (based on % dislikes) and news & politics videos the most negative sentiment on average
    - Most videos trend in less than a week after getting published, barring outliers
    - However, videos which take more than average time to trend - 4 to 7 days receive much higher views on average (barring videos which trend more than a week after getting published)
    - Videos published on working days (no holiday or weekend) seem to rack up marginally more views
    - Tags that show up the most for trending videos in India seem to be related to movies, music featured in movies, TV series with associated language indicated (Hindi, Tamil, etc.)
    - The most important factors in determining the number of views for a trending video seem to be the number of days it takes for the video to trend, the category of the video and the % dislikes that the video garners


## Acknowledgements

A big thanks to the Udacity team for setting up the motivation to do this by including "writing a blog post" as a project in the Data Science Nanodegree program. I found the youtube dataset an interesting one to explore after browsing through Kaggle datasets. Thank you Kaggle for hosting and user "datasnaek" for providing such an interesting dataset which motivated the analysis.
