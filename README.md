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

* I initialized the K-means model with the best value for k.
* I fit the K-means model using the original scaled DataFrame.
* I predicted the clusters to group the cryptocurrencies using the original scaled DataFrame.
* I created a copy of the original data and add a new column with the predicted clusters.
    * Sample code is as follows:

![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/80fdc872-e200-4a5f-b3fd-9fbc3b1839a9)

* I Created a scatter plot using hvPlot as follows:
    * Set the x-axis as "PC1" and the y-axis as "PC2".
    * Colored the graph points with the labels found using K-means.
    * Added the "coin_id" column in the hover_cols parameter to identify the cryptocurrency represented by each data point.

![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/907b02ad-416c-4b44-b3e0-0258c749e3d7)

## Optimizing Clusters with Principal Component Analysis.
I performed a PCA and reduce the features to three principal components using the original scaled DataFrame.

* I retrieved the explained variance to determine how much information can be attributed to each principal component
    * The total explained variance of the three principal components is 89.5% (the sum of the array of [0.3719856 , 0.34700813, 0.17603793]
    * Sample code:

![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/eb32bf4f-0a55-4a37-b3ff-245b47e5832f)

* Created a new DataFrame with the PCA data and set the "coin_id" index from the original DataFrame as the index for the new DataFrame.
    * The first five rows of the PCA DataFrame appeared as follows:
 

## Finding the Best Value for k Using the PCA Data
Similar to the original data, I used the elbow method on the PCA data to find the best value for k using the following steps:
* Created a list with the number of k-values from 1 to 11.
* Created an empty list to store the inertia values.
* Created a for loop to compute the inertia with each possible value of k.
* Created a dictionary with the data to plot the Elbow curve.
    * Sample code as follows:

![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/e354a5f5-3196-41b0-bf3b-ed9f9d3b9080)

![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/8c77df15-705a-4dd1-948c-a3738bf05258)

* Ploted a line chart with all the inertia values computed with the different values of k to visually identify the optimal value for k.
    * Line chart as follows:

![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/9ef1e70a-42a7-4c1c-b7f3-7187a122d736)

* After examining the elbow chart, the best value for k was 4 and it does not differ from the original data.

## Cluster Cryptocurrencies with K-means Using the PCA Data
I used the following steps to cluster the cryptocurrencies for the best value for k on the PCA data:
* I initialized the K-means model with the best value for k.
* I fit the K-means model using the PCA data.
* I predicted the clusters to group the cryptocurrencies using the PCA data.
* I created a copy of the DataFrame with the PCA data and add a new column to store the predicted clusters.
    * Sample code is as follows:
 
![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/206aaf48-f0f8-4187-a75b-652cbde6cefb)
  
* I created a scatter plot using hvPlot as follows:
    * I set the x-axis as "price_change_percentage_24h" and the y-axis as "price_change_percentage_7d".
    * I colored the graph points with the labels found using K-means.
    * I added the "coin_id" column in the hover_cols parameter to identify the cryptocurrency represented by each data point.
    * PCA plot is as follows:
![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/cbbff5fb-cef9-4629-9908-926c78d48175)

## Side-by-Side Analysis of the Original Scaled Data and the PCA data
* In the jupyter notebook, I compared the original scaled data and the PCA data by making a side-by-side comparison of the elbow curves and the scatter plots of the clusters.

![image](https://github.com/nicholaishaw/CryptoClustering/assets/135463220/c7999933-3083-4ad4-9900-3f11fb20e214)

## The impact of using fewer features to cluster the data using K-Means
There are several impacts of using fewer features to clusters. Firstly, it accelerates the K-Means function to make it more efficient—especially with large datasets. As such, since it is improbable to include every single column of data contributing to variance, the data need to be trimmed to only include the data contributing to most of the variance of the dataset. Secondly, using fewer features may result in less accurate cluster representations of the dataset. This can lead to a somewhat incomplete picture compared to using all available features.
