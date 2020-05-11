# DSCI_6007
Final Project on Netflix Recommendation System

## Motivation
Considering Data Engineering as an integral part of data world, Spark plays a big role in big data processing. The project on Netflix recommendation program was one of the top problems of last decade which made lot of noise in the tech world. Knowing the fact that the dataset has 3.25 million records makes it a good data engineering problem, using spark cluster and pythonic ways.

## Introduction
We all know recommendations system play a big part in online business specially e-commerce and streaming services. Companies need to recommend the products which would attract users and compel them to buy. Looking at the customer side, they want to get  recommendations based on their taste and liking.
The dataset consists of ratings given by users to different movies, also the details of the movies. It consists of a total 3.25 million records for training and 100,000 records for testing. In this case, collaborative filtering techniques like item-item filter and user-user filter to compare and use the best among them. Along with-it using cosine distance similarity between the records to give the best possible recommendations. Finally applying Alternating Least Squares algorithm to get the results. By doing this project, I got an idea about the entire workflow of a recommendation system.

## Approach

1.	Data Analysis:
	Once we have	imported the data from the S3 bucket into our spark cluster, we store all the data in spark dataframe. For our analytic use, convert the pyspark dataframe into pandas dataframe.
Trying to get to know how the data is spread, what kind of values are in, how many of them are present, etc. plays a very important role to understand what is to be done in the next steps like selecting an algorithm, number of iterations to done considering the size of the data and so on.
2.	Collaborative filtering approach
  These are the two different filtering approaches one can use to recommend any kind of thing. In this problem, we are using the collaborative approach to recommend Netflix shows/movies to different users.

In the collaborative approach, there are two different memory-based algorithms:
a.	User-User Collaborative Filtering: 

	In this approach, we try to find the users who are like a user we are trying to recommend for. So, here we try to maintain a matrix where we have info about the users and movies they have rated. If we are looking to recommend for user ‘x’ and we have user ‘y’ and ‘z’ who are somewhat similar to x, then we try to recommend movies watched by y and z, not by x. It is a very memory heavy approach and its necessary to have a powerful parallel execution capable machine/machines to make this work.

b.	Item-item Collaborative Filtering

    In this approach, we try to find the movies which are alike, and try to recommend movies which are similar to a specific movie. This approach is also done with the help of a matrix which has movies and their ratings are stored. It is comparatively less memory heavy and can give results faster as compared to the user-based filtering. Also, it does not require any similarity measure to be calculated for users which is computationally heavy.

    Here instead we calculate the distance between two movie pairs:

    In this problem, we are using the cosine distance metric:

    It is the cosine of the angle between the two vectors which are being considered.
    If the vectors are close than cosine value will be large. 

3.Implementing the algorithm using pyspark

The approach her is to apply the Alternating Least Squares method from the ML library of pyspark. Idea was to train the entire 3.25 million records and testing on the 100,000 records from test set. 

The algorithm has various hyper parameters like regParam, max iterations, user column, item column and rating column to create a matrix which can be used to recommend movies to the users. Fitting this model on the training data yields us an MSE value of 0.82 and RMSE value of 0.9.

 

4.	Testing by adding personal records

Created a text file consisting of 15 records and added it to the training data, then predicted the recommendations for me.

Conclusion and Future work

The most important thing we learnt in with this project is the importance of collaborative filtering techniques in recommendation system. Also, how spark plays a big role in providing the computational power to complete this heavy task.

Future work on this project can be applying different distance measures along with 
algorithms to see if we can get any better results.
