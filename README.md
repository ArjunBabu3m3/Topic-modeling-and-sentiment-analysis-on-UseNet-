# Topic-modeling-and-sentiment-analysis-on-UseNet-

![alt text](amazon.JPG)

### Table of contents
* [Introduction](#introduction)
* [Problem Statement](#problem-statement)
* [Data Source](#data-source)
* [Technologies](#technologies)
* [Type of Data](#type-of-data)
* [Data Pre-processing](#data-pre-processing)
* [Algorithms Implemented](#algorithms-implemented)
* [Steps Involved](#steps-involved)
* [Evaluation Metrics](#evaluation-metrics)
* [Results and Conclusion](#results-and-conclusion)

### Introduction
The objective of the project is to develop a product recommendation system based on the customer’s interest. The purchase history is retrieved to capture customer’s inclination for a set of products available in the store. The data extraction, exploration, transformation and analysis would be achieved through Apache Spark system. Based on the analysis, the system would recommend products for customers who would most likely be inclined to buy a set of products along with the current product picked up for check out. This recommendation system is intended to help e-commerce web sites to service customers with appropriate recommendations at the right time with an attractive price tag.

### Problem Statement
* Build a product recommendation system based on the customer’s interest.

### Data Source
* The Dataset was obtained from the website: https://nijianmo.github.io/amazon/index.html
  The data set is a part of Amazon review dataset released in 2014, provided by UCSD.

### Technologies
* Python 3.6.7
* PySpark 3.0.0

### Type of Data
* The data set contains data for 287,209 products with 5,074,160 reviews and ratings by 1, 57,386 unique users.
* The data does not contain any null values
* Train : 80%
* Test  : 20%

### Data Pre-processing
* Tokenizing, removal of stop words and stemming was done for textual data

### Algorithms Implemented
* K-Means (Context Based Filtering)
* ALS Collaborative Filtering Algorithm

### Steps Involved

## Technique 1 - K-Means(Context Based Filtering)
* Based on the reviews obtained above we have created its TF-IDF using TfidfVectorizer function.
* Since we are handling huge amount of data with our data frame having 5,074,160 reviews we have done rest of the operations in Apache Spark for efficient and faster handling of big data. We have created a Spark data frame from the pandas reviews data frame
* Next we have created a data cleaning pipeline using the Pipeline function in which we have cleaned the spark data frame by tokenizing the reviews, removing stop words, calculated the term frequencies (TF) and IDF for the tokenized words.
* We have clustered the products. So now whenever a new input keyword has been searched, it would pass through pipeline for cluster assignment. Products under the respective cluster are up for recommendation.

## Technique 2 - ALS Collaborative Filtering Algorithm
* We have obtained a Spark data frame containing item id, user id and ratings
* Alternating Least Squares algorithm requires the inputs to be numerical and integers with value less than 2,147,483,647 (32-bit limit). So we have created new index for      item_id and user_id using StringIndexer with definitive mapped values for each user and item.
* We have split the data into (80%) training and (20%) testing. We have used ALS (Alternating Least Squares) algorithm for training the data.
* We have evaluated the model on the test data. We have got RMSE value of 1.134. We thought that it might be over fitting the data so we implemented 5-fold Cross Validation in the next step.
* After implementing 5-fold ALS Cross Validation and evaluating on the test data we have obtained a RMSE value of 0.8345 which showed an improvement from the previous time.
* Finally, using our model we are obtaining TOP 10 recommendations for all the users in our data frame.
  
### Evaluation Metrics  
RMSE (Root Mean Square Error) 

### Results and Conclusion
By analyzing our dataset through various tools like R, Python, Pyspark we developed a product recommendation system based on the customer’s interest. We have used 2 different models for this purpose i.e. KNN and ALS Collaborative Filtering.

For the KNN which does context based filtering, we have tested our model with a test data which shows products under their respective cluster. It shows the products which are closely related to Kit Kat.

![alt text](rec_res1.JPG)

On implementing the ALS Collaborative Filtering Algorithm, we have used ALS model in which we have obtained RMSE value of 1.134.

![alt text](rec_res2.JPG)

On using 5-fold cross validation and evaluating on the test data the RMSE value showed an improvement. We obtained RMSE value of 0.8345.

![alt text](rec_res3.JPG)
