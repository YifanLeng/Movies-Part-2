# Movies-Part-2

## Algorithms
I designed three algorithms to predict a user(u)'s rating on a movie(m). The first one computes genre avergae rating of m, the second one computes the average rating of similar users to u, and the last one computes a weighted average from those two. 

### Genre Average Algorithm
This algorithm simply comptutes the average rating of movies with the same genre as m. We diregrad the user's information and only consider the movie that we try to predict. This serves to provide a baseline to compare with other algorithms.

### Similar User Average Algorithm
This algorithm simply computes the average rating of users similar to u. We disregard the movie's information and only consider the user that we try to predict. We define similar uses as users with the same occupation and gender as user u. 

## Weighted Average Algorithm
To predict rating of user (u) for movie (m), this algorithm tries to compute a weighted average of them = w_1 * avg(m) + w_2 * avg(u). W_1 and w_2 are hyperparameters that we can finetune later on. 

## Implementation

We will implement the algorithms with PostgreSQL database and Ruby's ActiveRecord interface with the database. We will migrate three tables into our psql database. 

Ratings:

| user_id      | item_id    | rating     |
| :------------- | :----------: | -----------: |

Movies:

| item_id      | movie_title    | genre_id     |
| :------------- | :----------: | -----------: |

Users:

| user_id     | gender    | occupation     |
| :------------- | :----------: | -----------: |

We precomputed the two average rating tables as follows:

Genre Averages:

| genre_id     | gender_average   | 
| :------------- | :----------: | 

Similar User Averages:

| gender    | occupation    | user_average     |
| :------------- | :----------: | -----------: |



