# Crypto Clustering Analysis Using K-Means

In this challenge, I used my knowledge of Python and unsupervised learning to predict if cryptocurrencies are affected by 24-hour or 7-day price changes.

## Preparing the Data
* Data were imported from the csv file containing information on the prices of crypto currency and put into a Pandas dataframe.
    * The raw dataframe is as follows:
 
![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/fb97d976-738c-4b69-9990-19817a19d294)

* Data were graphed to highlight the price change of each bitcoin across various timepoints
    * Plot is as follows:

![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/455214b6-53c4-4e72-818e-c5fd51f36455)

* I used the StandardScaler module from the scikit-learn library to normalize the data from the raw CSV file.
* I created a DataFrame with the scaled data and set the "coin_id" index from the original DataFrame as the index for the new DataFrame.
    * The first ten rows of the scaled DataFrame is as follows:
 
![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/66dd83ef-d6c3-4365-a18e-9b8aaee21756)

## Finding the Best Value for k Using the Original Scaled DataFrame
I Used the elbow method to find the best value for k using the following steps:

* I created a list with the number of k values from 1 to 11.
* I created an empty list to store the inertia values.
* I created a for loop to compute the inertia with each possible value of k.
    * Sample code is as follows:
 
![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/a45f6ee9-5c16-4d60-bf57-647f48b4f7d6)

* I created a dictionary with the data to plot the elbow curve.
    * Sample code as follows:

![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/9528429f-c30a-4450-a8c6-2b6dfb1b52eb)

* I plotted a line chart with all the inertia values computed with the different values of k to visually identify the optimal value for k.
    * Line chart as follows:

![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/f8627ff6-e1d0-4962-b6f7-ad1823968014)

* After carefully examining the elbow chart, the best value for k was 4—the point where the graph runs almost parallel to the x-axis

## Clustering Cryptocurrencies with K-means Using the Original Scaled Data
I used the following steps to cluster the cryptocurrencies for the best value for k on the original scaled data:

* Initialized the K-means model with the best value for k.
* Fit the K-means model using the original scaled DataFrame.
* Predicted the clusters to group the cryptocurrencies using the original scaled DataFrame.
* Created a copy of the original data and add a new column with the predicted clusters.
* Created a scatter plot using hvPlot as follows:
    * Set the x-axis as "PC1" and the y-axis as "PC2".
    * Colored the graph points with the labels found using K-means.
    * Added the "coin_id" column in the hover_cols parameter to identify the cryptocurrency represented by each data point.

## Optimizing Clusters with Principal Component Analysis.
I performed a PCA and reduce the features to three principal components using the original scaled DataFrame.

* Retrieved the explained variance to determine how much information can be attributed to each principal component
    * The total explained variance of the three principal components is 89.5% (the sum of the array of [0.3719856 , 0.34700813, 0.17603793]
* Created a new DataFrame with the PCA data and set the "coin_id" index from the original DataFrame as the index for the new DataFrame.
    * The first five rows of the PCA DataFrame should appear as follows:
 
![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/08a7e784-552b-40fd-9426-6bccd4cc0fca)

## Finding the Best Value for k Using the PCA Data
Used the elbow method on the PCA data to find the best value for k using the following steps:
* Created a list with the number of k-values from 1 to 11.
* Created an empty list to store the inertia values.
* Created a for loop to compute the inertia with each possible value of k.
* Created a dictionary with the data to plot the Elbow curve.
    * Sample code as follows:



* Ploted a line chart with all the inertia values computed with the different values of k to visually identify the optimal value for k.
    * Line chart as follows:



* After examining the elbow chart, the best value for k was 4 and it does not differ from the original data.

## Cluster Cryptocurrencies with K-means Using the PCA Data
Used the following steps to cluster the cryptocurrencies for the best value for k on the PCA data:
* Initialized the K-means model with the best value for k.
* Fit the K-means model using the PCA data.
* Predicted the clusters to group the cryptocurrencies using the PCA data.
* Created a copy of the DataFrame with the PCA data and add a new column to store the predicted clusters.
* Created a scatter plot using hvPlot as follows:
* Set the x-axis as "price_change_percentage_24h" and the y-axis as "price_change_percentage_7d".
* Colored the graph points with the labels found using K-means.
* Added the "coin_id" column in the hover_cols parameter to identify the cryptocurrency represented by each data point.
* Answer the following question:

## The impact of using fewer features to cluster the data using K-Means
There are several impacts of using fewer features to clusters. Firstly, it accelerates the K-Means function to make it more efficient—especially with large datasets. As such, since it is improbable to include every single column of data contributing to variance, the data need to be trimmed to only include the data contributing to most of the variance of the dataset. Secondly, using fewer features may result in less accurate cluster representations of the dataset. This can lead to a somewhat incomplete picture compared to using all available features.
