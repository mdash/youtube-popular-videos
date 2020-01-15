# Analysis of trending videos on Youtube India

Analysis of trending videos data from Youtube. Please check out the [blog post](https://medium.com/@md047/what-are-the-types-of-videos-that-trend-on-youtube-cadcebf51115). 

## Objective

The objective is to tease out simple relationships within trending YouTube videos in India based on the available data.

## Approach

- Simple EDAs with distributions of the various features
- Modeling the # views that trending videos get against the features
- SHAP and PDP plots to quantify the impact of the features against the # views that a video gets

## Data source

1. Trending videos data sourced from Kaggle - [link](https://www.kaggle.com/datasnaek/youtube-new). Required files:
- IN_category_id.json
- INvideos.csv

2. India holidays data sourced from https://www.timeanddate.com/holidays/india
- ./data_pull/holidays_india_17_18.csv

## Acknowledgements

A big thanks to the Udacity team for setting up the motivation to do this by including "writing a blog post" as a project in the Data Science Nanodegree program. I found the youtube dataset an interesting one to explore after browsing through Kaggle datasets. Thank you Kaggle for hosting and user "datasnaek" for providing such an interesting dataset which motivated the analysis.
