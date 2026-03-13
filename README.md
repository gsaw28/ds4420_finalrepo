# DS 4420 - Final Project 
## Predicting Steam Game Prices Using Machine Learning
Authors: Gianna Saw, Jason Zheng 

## Project Overview 
The project is centered on the following question: to what extent can a game's content, quality, and engagement metrics be used to predict its price on the Steam marketplace? 

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
No pre-built modeling packages (e.g. scikit-learn) are used — all forward pass, backpropagation, and gradient descent logic is implemented from scratch.
- **Language:** Python
- **Libraries:** NumPy, Pandas

### Model 2: Bayesian Linear Regression
A Bayesian regression model that predicts game price while  providing posterior uncertainty estimates on coefficients. This allows for probabilistic interpretation of how each  game feature influences price, rather than a single point estimate.
- **Language:** R
- **Libraries:** brms / rstan
- **Implementation:** Package-based

## Repository Structure 
- poc_data_processing.ipynb -- preprocessing methods
- steam_clean.csv -- cleaned dataset (40k rows) with specific features we need
- poc_train.ipynb -- training methods for POC demonstration





