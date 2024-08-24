# Movie Recommendation System using SVD

This repository contains a script to build a movie recommendation system using Singular Value Decomposition (SVD) with the Surprise library. The system is designed to provide personalized movie recommendations for users based on their historical ratings.

## Table of Contents

- [Movie Recommendation System using SVD](#movie-recommendation-system-using-svd)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Dataset](#dataset)
  - [Requirements](#requirements)
  - [Installation](#installation)
  - [Usage](#usage)
  - [How It Works](#how-it-works)
  - [Example Output](#example-output)
  - [Contributing](#contributing)

## Overview

This project demonstrates a basic recommendation system using collaborative filtering techniques. The system predicts user ratings for movies they have not yet rated and recommends the top N movies based on these predictions.

## Dataset

The MovieLens 100k dataset is used in this project. It consists of 100,000 ratings (1-5) from 943 users on 1682 movies.

- **Ratings file**: [u.data](http://files.grouplens.org/datasets/movielens/ml-100k/u.data)
- **Movie titles file**: [u.item](http://files.grouplens.org/datasets/movielens/ml-100k/u.item)

## Requirements

- Python 3.x
- pandas
- scikit-surprise

## Installation

To run the script, you need to install the required Python libraries. You can install them using `pip`:

```bash
pip install pandas scikit-surprise
```

## Usage

1. **Clone the repository**:

```bash
git clone https://github.com/yourusername/movierecommendation.git
cd movierecommendation
```

2. **Run the script**:

```bash
python recommend.py
```

## How It Works

1. **Load the Data**: The script first loads the MovieLens dataset (both the user ratings and movie metadata) into pandas DataFrames.

   ```python
   df = pd.read_csv(url_data, sep="\t", names=column_names)
   df_movies = pd.read_csv(url_item, sep="|", names=movie_columns, encoding="latin-1")
   ```

2. **Preprocessing**: The data is then converted into a format suitable for the Surprise library. The `Reader` class helps define the rating scale.

   ```python
   reader = Reader(rating_scale=(1, 5))
   data = Dataset.load_from_df(df[["user_id", "item_id", "rating"]], reader)
   ```

3. **Train-Test Split**: The dataset is split into training and testing sets to evaluate the performance of the recommendation system.

   ```python
   trainset, testset = train_test_split(data, test_size=0.2)
   ```

4. **Model Training**: The SVD algorithm is used to train the model on the training data.

   ```python
   model = SVD()
   model.fit(trainset)
   ```

5. **Model Evaluation**: The trained model is evaluated on the test data using Root Mean Square Error (RMSE).

   ```python
   predictions = model.test(testset)
   accuracy.rmse(predictions)
   ```

6. **Making Recommendations**: A function `recommend` is defined to predict the top N movie recommendations for a given user.

   ```python
   def recommend(user_id, num_recommendations=5):
       # Logic to generate top N recommendations
   ```

## Example Output

When the script is run, it outputs the RMSE score and provides the top 5 movie recommendations for a specified user. Below is an example of the output:

```
RMSE: 0.9234
Top 5 recommendations for user 196:
1. Star Wars (1977): Predicted Rating 4.82
2. Raiders of the Lost Ark (1981): Predicted Rating 4.67
3. Fargo (1996): Predicted Rating 4.59
4. Return of the Jedi (1983): Predicted Rating 4.56
5. The Godfather (1972): Predicted Rating 4.55
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
