# DS 4420 - Final Project 
## Predicting Steam Game Prices Using Machine Learning
Authors: Gianna Saw, Jason Zheng 

## Project Overview 
The project is centered on the following question: to what extent can a game's content, quality, and engagement metrics be used to predict its price on the Steam marketplace? 

## Interactive Website for Extension Points (2)
https://steam-dataset-9lmxpl7o3jo.streamlit.app 

## Description 
This question lies at the intersection of digital platform economics and machine learning. Pricing decisions on large global platforms such as Steam can have significant implications for the thousands of independent developers who release games each year, as price influences both market positioning and consumer demand.

## Dataset
The project uses this existing [Steam dataset ](url). Data has been scraped using Steam API, the largest gaming platform on PC. It has 120k data rows, which is an ideal number for the ML tests we will be conducting. 

The dataset contains several game-related pieces of information: 
- Identity/Basic Info
  - appID — unique game identifier
  - name — game name
  - release_date — release date
- Target Variable (for the purposes of our project) 
  - price — game price (this is what you're predicting)
- Engagement/Popularity Metrics
  - peak_ccu — peak concurrent users
  - estimated_owners — estimated ownership range
  - average_playtime_forever — average playtime all time
  - average_playtime_2weeks — average playtime last 2 weeks
  - median_playtime_forever — median playtime all time
  - median_playtime_2weeks — median playtime last 2 weeks
  - recommendations — number of recommendations
- Review/Rating Info
  - positive — number of positive reviews
  - negative — number of negative reviews
  - user_score — user score
  - metacritic_score — metacritic score
  - metacritic_url — metacritic link
  - score_rank — score ranking
  - reviews — review text
- Game Content Features
  - dlc_count — number of DLCs
  - achievements — number of achievements
  - required_age — age rating
- Platform Support
  - windows — supports Windows
  - mac — supports Mac
  - linux — supports Linux
- Categorical/List Features
  - genres — game genres
  - categories — Steam categories (multiplayer, co-op, etc.)
  - tags — user-assigned tags
  - developers — developer name(s)
  - publishers — publisher name(s)
  - supported_languages — list of supported languages
  - full_audio_languages — languages with full audio
- Text/Media
  - detailed_description — long description
  - short_description — short description
  - header_image — image URL
  - screenshots — screenshot URLs
  - movies — trailer URLs
  - website — game website
  - support_url / support_email
  - notes — additional notes
  - packages — pricing package details

For our models, the most useful features will be: genres, tags, metacritic_score, positive, negative, dlc_count, achievements, average_playtime_forever, required_age, categories, and peak_ccu

## Methods  
In predicting prices, we will be using MLP NN and Bayesian Linear Regression. 

### Model 1: MLP NN
A feedforward neural network implemented manually using NumPy. 
The model takes game metadata as input and outputs a predicted price. 

### Model 2: Bayesian Linear Regression
A Bayesian regression model that predicts game price while  providing posterior uncertainty estimates on coefficients. 
This allows us to see a probabilistic interpretation of how each  game feature influences price, rather than a single point estimate.


## Repository Structure 
Files used for proof of concept (phase I) 
- poc_data_processing.ipynb -- preprocessing methods
- poc_train.ipynb -- training methods for POC demonstration

Final Files (Phase II): 
- Model1_Vfinal2.ipynb -- Model 1 (MLP) code
- Model2_Vfinal_2cleaned.Rmd -- Model 2 (Bayesian) R code
- Model2_Vfinal.pdf --  R code, but exported to pdf
- Steam_clean_v2.csv -- updated dataset
- EDA -- EDA code for research

## Explaining Pivot from `steam_clean_v1.csv` to `steam_clean_v2.csv`
**Authors: Gianna Saw, Jason Zheng**

### Why we pivoted
We moved from `steam_clean_v1.csv` to `steam_clean_v2.csv` because our first preprocessing pass was useful for a proof of concept, but it still left important data-quality and feature-representation issues that limited model reliability.

In v1, we reduced the table to a compact numeric set and filtered to paid games, but:
- list-like fields were not always parsed consistently (`Supported languages` often became `0` in practice),
- ownership ranges were not robustly converted to numeric signal,
- category/genre encoding was only partially integrated into the final training table,
- sparse score fields (Metacritic/User score) did not explicitly distinguish “missing” from true zero,
- and we ended with a smaller feature space (about **40,677 rows × 19 columns**) that was easier to train, but less expressive.

### What changed in v2
In `steam_clean_v2.csv`, we rebuilt preprocessing with stronger structure and consistency:
- standardized the input from the newer Steam dataset format,
- dropped non-modeling metadata fields (descriptions, URLs, media links, etc.),
- converted `estimated_owners` range strings to numeric midpoints, then log-transformed,
- added robust `language_count`,
- converted platform booleans (`windows`, `mac`, `linux`) to integer flags,
- added sparsity indicators (`has_metacritic`, `has_user_score`) so missing-score behavior is model-visible,
- one-hot encoded genre information directly into the final modeling table,
- log-transformed skewed engagement/playtime predictors and price,
- filtered to paid titles for consistent paid-price modeling.

This produced a richer and cleaner matrix (about **97,734 rows × 54 columns**), improving both feature coverage and downstream stability for Model 1 (MLP) and Model 2 (Bayesian tier model).






