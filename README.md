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

## Analysis and Benchmarking

A typical error and time analysis on u4.base and u4.test is as follows:

```
Current Time : 2020-01-28 01:21:59 -0500
using u4.base and u4.test
Results of the genre average
Count of predictions off exactly by 1 is 9722.
The mean error of the predictions is 0.47815.
The standard deviation of the errors is 1.113276491590214.
Results of the user average
Count of predictions off exactly by 1 is 9667.
The mean error of the predictions is 0.45205.
The standard deviation of the errors is 1.112727597229255.
Results of the weighted average
Count of predictions off exactly by 1 is 9712.
The mean error of the predictions is 0.4705.
The standard deviation of the errors is 1.1089144396939439.
Current Time : 2020-01-28 01:23:25 -0500

```

A typical running time of training and testing with all three algorithms is 84 seconds. The error logs of some other batches are as follows:

```
using u1.base and u1.test
Results of the genre average
Count of predictions off exactly by 1 is 9639.
The mean error of the predictions is 0.4641.
The standard deviation of the errors is 1.153680085156646.
Results of the user average
Count of predictions off exactly by 1 is 9626.
The mean error of the predictions is 0.454.
The standard deviation of the errors is 1.1456219369763487.
Results of the weighted average
Count of predictions off exactly by 1 is 9634.
The mean error of the predictions is 0.4614.
The standard deviation of the errors is 1.1491196908080743.

```
```
using u2.base and u2.test
Results of the genre average
Count of predictions off exactly by 1 is 9678.
The mean error of the predictions is 0.45655.
The standard deviation of the errors is 1.1305644635757424.
Results of the user average
Count of predictions off exactly by 1 is 9702.
The mean error of the predictions is 0.4352.
The standard deviation of the errors is 1.11564474325804.
Results of the weighted average
Count of predictions off exactly by 1 is 9676.
The mean error of the predictions is 0.45205.
The standard deviation of the errors is 1.124306008478276.
```

```
using u3.base and u3.test
Results of the genre average
Count of predictions off exactly by 1 is 9662.
The mean error of the predictions is 0.47505.
The standard deviation of the errors is 1.111593126761881.
Results of the user average
Count of predictions off exactly by 1 is 9634.
The mean error of the predictions is 0.44.
The standard deviation of the errors is 1.1062374013110132.
Results of the weighted average
Count of predictions off exactly by 1 is 9645.
The mean error of the predictions is 0.46435.
The standard deviation of the errors is 1.1053914112242134.
```

The time of training and testing will grow more than linearly with the data size. When the data is ten times the size of the current, the trainig and testing will take moe than 10 times than its current time cost.

## Reflection

I enjoyed most about learning Daru as a subtitute of pandas in Ruby. When the data size grows, we can consider using database such as PostgreSQL and ActiveRecord to perform storing, joining and aggregating operations.






