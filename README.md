# Analysis-of-Different-Movie-recommendation-systems
This Project deals with Analysis of three types of Recommendation Systems namely, Demographic Filtering, Content Based Filtering and Collaborative Filtering. This uses the Movies Dataset (Metadata on over 45,000 movies. 26 million ratings from over 270,000 users).

# Analysis of Movie recommendation systems on The Movie Dataset. 
This contains Metadata on over 45,000 movies. 26 million ratings from over 270,000 users.

Methods Used -

## 1. Demographic Filtering- 
They offer generalized recommendations to every user based on movie popularity and/or genre. The System recommends the same movies to users with similar demographic features. Since each user is different, this approach is considered too simple. The basic idea behind this system is that films that are more popular and critically acclaimed will have a higher probability of being liked by the average audience.

Steps involved-
* We calculate a metric to score or rate a movie
* Calculate the score for every movie
* Sort the scores and recommend the best-rated movie to the users

We will use the Weighted Rating IMDB used to calculate the Metric used to Score/ rate a Movie. 

![image](https://user-images.githubusercontent.com/88557375/205922923-08f964a0-1b6d-4f4a-88b0-9a073a66fed2.png)

where,
* v is the number of votes for the movie
* m is the minimum number of votes required to be listed in the chart
* R is the average rating of the movie
* C is the mean vote across the whole report

The calculated Mean Rating for the Movies is 3.49205 on a scale of 0-5.

The next step is determining an appropriate value for m, the minimum votes required to be listed in the chart. We will use the 90th percentile as our cutoff.

We see that 1001 movies qualify to be on this list. Now, we need to calculate our metric for each qualified movie. To do this, we will define a function, weighted_rating(), and define a new feature score, of which we'll calculate the value by applying this function to our DataFrame of qualified movies:

![image](https://user-images.githubusercontent.com/88557375/205941677-bddb9ccf-6759-4afc-86df-a3b6656ea33d.png)

Now, we sort the Movies according to the ratings giving the result as follows -

![image](https://user-images.githubusercontent.com/88557375/205942096-05781635-ae76-483f-8641-833fddc401e9.png)



## 2. Content-Based Filtering- 
They suggest similar items based on a particular item. This system uses item metadata, such as genre, director, description, actors, etc., for movies to make these recommendations. The general idea behind these recommender systems is that if a person likes a particular item, he or she would also like an item similar to it.

In this recommender system, the movie's content (overview, cast, crew, keyword, tagline, etc.) is used to find its similarity with other movies. Then the movies that are most likely to be similar are recommended.

Now, we will calculate Term Frequency-Inverse Document Frequency (TF-IDF) vector for the overview. We calculate TF-IDF by using built-in TFldfVectorizer by scikit-learn.
In our Matrix, we see that over 32,000 words are used to describe over 10000 movies. 
(Here, I have considered the top 10,000 movies because I do not have the processing power required for the complete Dataset).

We will use the cosine similarity to calculate a numeric quantity that denotes the similarity between two movies. We use the cosine similarity score to calculate the same.

![image](https://user-images.githubusercontent.com/88557375/205954208-fc4e1d9a-1b9d-428c-b8e3-77e45071bdb1.png)
 
Since we have used the TF-IDF vectorizer, calculating the dot product will directly give us the cosine similarity score. Therefore, since it is faster, we will use sklearn's linear_kernel() instead of cosine_similarities().

We will define a function that takes in a movie title as an input and outputs a list of the 10 most similar movies. Firstly, we need a reverse mapping of movie titles and DataFrame indices. In other words, given its title, we need a mechanism to identify the index of a movie in our metadata DataFrame.

We are now in an excellent position to define our recommendation function. These are the following steps we'll follow:-

* Get the index of the movie given its title.
* Get the list of cosine similarity scores for that movie with all movies. Convert it into a list of tuples where the first element is its position and the second is the similarity score.
* Sort the list above of tuples based on the similarity scores, that is, the second element.
* Get the top 10 elements of this list. Ignore the first element as it refers to self (the movie most similar to a particular movie is the movie itself).
* Return the titles corresponding to the indices of the top elements.

![image](https://user-images.githubusercontent.com/88557375/205954818-5f255ccb-7a5c-4261-91e8-10a0ed310016.png)

## 3. Collaborative Filtering- 
This system matches persons with similar interests and provides recommendations based on this matching. Collaborative filters do not require item metadata like their content-based counterparts.

![image](https://user-images.githubusercontent.com/88557375/206236614-9c88fe38-9597-49db-b41e-4be8e7a17b21.png)

Based on the plot produced by the Plotly code, we can see that the points representing the 33,000 movies seem to follow a two-dimensional normal distribution. We can explain this distribution with the following theories about the movies in the dataset:

Some movies may be generally popular among a wide range of audiences and thus correspond to points in the center of this scatterplot.
Other movies may fall into particular genres, such as vampire novels, mystery novels, and romance, that are popular among specific audiences. These movies may correspond to points away from the center of the plot.


