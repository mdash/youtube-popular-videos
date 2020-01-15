# Analysis of trending videos on Youtube India

Analysis of trending videos data from Youtube. Please check out the [blog post](https://medium.com/@md047/what-are-the-types-of-videos-that-trend-on-youtube-cadcebf51115). 

## Objective

The objective is to tease out relationships within trending YouTube videos in India based on the available data.

## Approach

Broadly the following approach was adopted:

    - EDAs with distributions of the various features
    - Modeling the # views that trending videos get against the features
    - SHAP and PDP plots to quantify the impact of the features against the # views that a video gets

CRISP-DM framework was used to answer the following questions:

1. What are the categories of trending videos?    
    - Business Understanding: The category of videos represent the genre of the video and is an essential classification that when explored gives an idea of what youtube users in India are generally interested in. 
    - Data Understanding: For answering this question, the entire dataset of trending videos from the 2017-18 timeframe was used and the # of occurences of each category of video in the trending list was evaluated.
    - Descriptive Analysis: Barplots were used to evaluate the # videos in a category that show up in the trending list of videos in the timeframe of the data.

2. What is the general sentiment towards trending videos?
    - Business Understanding: The number of likes that a video gets represents the general sentiment of the viewer towards the video or the issue characterized by the video. This helps gauge if some categories of videos are unanimously liked by the public or vice-versa.
    - Data Understanding: The data for trending videos captures the # likes and # dislikes garnered by the trending videos, which gives an idea of the viewer sentiment.
    - Prepare Data: % likes that a video gets is calculated based on number of likes / (number of likes + number of dislikes) and aggregated to the video category level for analysis.
    - Descriptive Analysis: Barplots are used to evaluate the distribution of % likes aggregated by video category against each other.
3. Does my old video still have a chance of trending?
    - Business Understanding: Although the metrics used by YouTube to put a video on the trending list aren't explicitly mentioned, a video that is listed on the trending page has a high likelihood of success and outreach (# users who view the video after it gets posted on the list). Evaluating when the video trended against when it was published gives an idea of the recency of videos on the trending list. 
    - Data Understanding: The data provides the publish time nad the trending date. The difference of these two date/time signatures gives the time that the video took in days to be added to the trending list.
    - Prepare Data: As mentioned in the previous point, days to trending is calculated as the difference between publish date and trending date.
    - Descriptive Analysis: Distribution plots of the days to trending metric gives an idea of the overall representation of videos based on the recency of getting published.
4. When are the most popular videos published?
    - Business Understanding: We might expect that the videos that get published during holidays/weekends are likely to get more visibility on the website due to the amount of free time that the users can spend on the website. To evaluate the hypothesis, it makes sense to look at the when the day that the video was published. 
    - Data Understanding: The data provides the date and time when the video was published.
    - Prepare Data: The video publish time is converted to IST timezone and a few features are extracted from this for analysis - the occurence of weekend/holiday on the day the video was published, time of the day the video was published (morning, afternoon, evening or night) and the month of the year that the video was published in. 
    - Descriptive Analysis: The metrics listed in the previous points are visualized through barplots and distributions looked at for testing out the hypothesis.
5. What are the most frequent tags attributed to trending videos?
    - Business Understanding: The tags attributed to videos are a more granular look at the content type of the video - going one level deeper than the explicit category of video available in the data. These help us identify subsegments within the broader video categories that youtube users in India area leaning towards more.
    - Data Understanding: The data provides video tags in pipe-separated format for each of the trending videos.
    - Prepare Data: The video tag provided in tabular format (as a pipe separated value) is tokenized. The occurence of word tags in the trending videos is analyzed by aggregating the video level occurence of these tags.
    - Descriptive Analysis: A word cloud visualization is used to look at the top video tags across the trending videos.
6. Which of these factors is more important?
    - Business Understanding: The # views that a video gets on youtube is a direct measure of the success of the video. The objective with this question, was to understand what were the characteristics of the trending videos that got more views. 
    - Data Understanding: The data prepared for answering all the previously listed business questions gives a good starting point for evaluating this.
    - Prepare Data: The data is split into training and testing sets (20% test), with the target variable being the number of views and the independent variables all the other non-ID features in the dataset prepared to answer the previous business questions.
    - Data Modeling: A LightGBM model was used to regress the target against the features. The model implicitly handles categorical and numeric features without a fuss, reducing the overhead on data preprocessing.
    - Evaluate the Results: For evaluation of early stopping criteria for the LightGBM model, RMSE was used as a loss function. Also, a GridSearch was run for hyperparameter tuning for the LightGBM model based on a Sci-kit Learn implementation. With the GridSearch implementation, the aim was to find the best values for ```num_leaves```, ```max_depth``` and ```learning_rate``` parameters of the model to ensure generalizability of the model wasn't sacrificed. SHAP plots and PDP were used for evaluation of the interactions of features with the target and interpretation of results.  


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

- A big thanks to the Udacity team for setting up the motivation to do this by including "writing a blog post" as a project in the Data Science Nanodegree program.
- I found the youtube dataset an interesting one to explore after browsing through Kaggle datasets. Thank you Kaggle for hosting and user ```datasnaek``` for providing such an interesting dataset which motivated the analysis.
- A shoutout to stackoverflow users [joe-kington](https://stackoverflow.com/users/325565/joe-kington) and [jsgounot](https://stackoverflow.com/users/5016055/jsgounot) for their answers which were used in the code (also referenced in docstring of the code)
