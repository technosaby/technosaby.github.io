---
layout : single 
title: Machine Learning 
permalink: /projects/ml/unsupervised_learning
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
toc: true
toc_label: "Unsupervised Algorithms"
author: Sabyasachi Ghosal
sidebar:
  nav: others_nav
---

# Datasets
To study unsupervised learning in this project, I have selected 2 datasets of different types. My first dataset is [Wine Dataset from UCI](https://archive.ics.uci.edu/ml/datasets/wine), which is more like a toy dataset, where there are 178 instances and 13 attributes. So, there is a chance that this dataset may face the curse of dimensionality because of having so many attributes but a smaller number of instances. This dataset contains all non-categorical or real variables. This dataset identifies different classes of wine based on their chemical composition. The class of the wine is defined by the customer segmentation data. This dataset has very well distributed 3 segments of customers (59, 71, 48). So, this dataset should ideally have 3 clusters in an unsupervised approach. But   it will be interesting to see that if any chemical component (or feature) really influences the formation of a cluster. 
I also wanted to study how unsupervised learning behaves on categorical data, so my second dataset is a [Mushroom Dataset from UCI](https://archive.ics.uci.edu/ml/datasets/mushroom). This dataset mainly identifies whether a type of mushroom can be poisonous, or edible based on the characteristics of the mushroom (like ring-type, habitat etc). Here I am considering a processed data set from Kaggle because it contains the classification types as edible and poisonous. It is a big dataset with 8124 instances and 22 attributes. In the dataset information from UCI, it also mentions about 3 classification types of them as definitely edible, definitely poisonous or unknown edibility and not recommended. So, it will be interesting to see whether the clustering actually points to 2 or 3 datasets. 

# Clustering Algorithm
## k-Means/k-Modes Clustering:  
For dataset1, I am using k-Means to understand the clusters. As my second dataset contains categorical variables, I am using k-Modes instead of k-Means. This is because k-Means always use Euclidean distance function which may not be applicable to categorical variables which are in a discrete space and the data has no natural origin. K-Modes works on a simple matching dissimilarity measure (hamming distance) for categorical objects and thus uses modes instead of means for clusters. For learning the data, I am removing the labels from the data and clustering them for different cluster sizes. After analysing the clusters, I select the optimised cluster and run some performance test on them. 
### Learning k 
#### Dataset 1
Silhouette Method: Among the different methods available to learn k, this method is one of the popular one. This method is a measure of how an object is similar to its own cluster compared to the other. Thus, objects with high Silhouette value are generally well clustered. From the silhouette plots for different clusters(k) as 2, 3, 4, 5, 6, 7, it is seen that in case of k=2,3, the thickness is uniform which gives an idea how balanced the clusters are. For k>3, wide fluctuations are seen in the size of the silhouette plots. For k = 3, the Silhouette value is the largest (0.30). 
Elbow Method This method provides the value of the cost function for different k values. Though elbow method provides a dirty heuristic, but here it is seen to find the right number of clusters pretty well. As seen in the plot above, at k=3, there is the point for the elbow.
![k means](/assets/images/ml_assets/ml_kmeans_wine_data.png)

#### Dataset 2
For learning k in the mushroom dataset, I am using the clustering cost. The clustering cost for k-Modes is the sum distance of all points to their respective cluster centroids. Thus, if the cost function is less, then there are more cluster groups, but there is chance of overfitting and if it too less, then we might not be finding the correct subsets, rather the supersets. Here in the cost function curve it is seen that the cost decreases rapidly with the increase of clusters. At k = 4, the cost function tends to decrease at a slower rate. Again, when k = 7, the cost function increases. So, it is better we don’t consider clusters more than that. It is very clearly visible that when the mushroom types are poisonous or edible, the cost function is high. But there is a chance that mushroom data can be neither poisonous nor edible which consists of the third cluster. 
![k means clusters](/assets/images/ml_assets/ml_num_clusters_mushroom_data.png)

## Description of the clusters
For wine data (set 1), I plotted a scatter plot with k=3 to see the distribution of the clusters for 2 feature spaces. From the graph, it is seen that the clusters can be distinctly identified. The centroids are also easily identified are far from each other showing a balanced distribution of data. The plotting can change based on the feature space selection, which I have not studied here. 

For the mushroom data (set 2), I have tried to plot the varying number of instances which gets classified based on the clusters. When the number of clusters (k) = 2, it is in 5:3 ratio. When k = 3, it changes from 4: 3: 1.5, which is a balanced one.  With the increase of the clusters the balance seems to lose and when it increases to 13, it becomes a kind of overfitting of the clusters. 
![k modes](/assets/images/ml_assets/ml_kmodes.png)

## Expectation Maximization
Like k-Means, I am trying to learn the model but by using the Gaussian mixture model with varying component/cluster value for both the datasets.
### Learning components
I have used the information-theoretic criteria or BIC to do the model selection for both the datasets. Among the many criteria available, BIC is the most efficient method to select the clusters. It assumes that the data is independently and identically distributed from a mixture of Gaussian. BIC is normally defined as, {-2 * loglik + nparams * log(n)}, where "loglik" is the log likelihood, "n" is the number of observations and "nparams" is the number of parameters. I am using Gaussian mixture model selection for learning the number of components as this concerns both the covariance type and the number of components in the model.
For the Wine data (set 1), the BIC score, for the Gaussian Mixture model selection with 3 components and covariance type as diagonal seems to perform the best. For the mushroom data (set 2), model with 5 clusters seem to perform the best. The * in the image shows the best model. 
![em components](/assets/images/ml_assets/ml_em_components.png)

### Description of Clusters
For the Wine data (set 1), I have plotted the clusters with k=3. It I compare it with that of k-Means, it is seen that in case of EM, the clusters are not bounded by hard-edge, but rather by a smooth one. When the number of components is 3, the red point which is a point between two clusters (yellow and green) has a probability of [0.32, 0.67, 3.1e-16]. This shows that the point is closer to the green cluster (0.67) than the yellow (0.32). Though it is not in the indigo cluster, it still assigns a very small probability to it. On the other hand, the blue is a point correctly placed between the indigo cluster is having the probabilities of [0.999, 2.86e-10, 4.07e-19].

![Em clusters](/assets/images/ml_assets/ml_clusters_wine_data_em.png)

## Dimensionality Reduction Algorithms
### Principal Component Analysis (PCA )
PCA is used to decompose a multivariate dataset in a set of successive orthogonal components that explain a maximum amount of the variance by transforming the features into different eigen values. The bar graph on the left shows the decay in variance for different components. For the wine data (set 1), the 1st and 2nd component contributes 0.40 and 0.19 (or 60% of total distribution), while 3 components explain around 68% of total distribution.  
I selected the higher eigen value components and throw away the ones which are low from the orthogonal components found by PCA. The eigen values reflect the portion of variance explained by the corresponding component. But I also wanted to understand the contribution of features in the selection of eigen vectors. So, I tried to plot the eigen vectors, considering 1PCA and 2PCA because from 3rd components the variance contribution becomes very low. The figure is shown on the right.
Here it is seen that the feature 5 [Weight: 0.1 + 0.3] & 8 [Weight: 0.1 + 0.5] are having highest weights and contribute more towards the 2 principal components. When I investigated the datasets, these can be features like ORD280 which actually helps in segmenting the user segment based on its chemical composition of the wine. 
![PCA Wine Data](/assets/images/ml_assets/ml_pca_components_wine_data.png)

For the mushroom data (set 2), I tried to plot the explained variance score for different number of principal components. It is true that when the number of components is 2, the variance is less. With the increase in principal components to 15, there are more dimensions to the model and thus it explained variance increases. When the number is 10, it contains around 90% of the variance. Thus, by reducing the dimensions from 22 to 10 we are making the model more simple. It is also important to notice the behaviour of the Eigen values. As expected, the eigen values will decrease with the increase of the principal components. When the number of components is 10, the eigen values decreased from 175 to 60, which is quite good for the dimension reduction.

![PCA Mushroom Data](/assets/images/ml_assets/ml_pca_mushroom_data.png)

###  Independent Component Analysis (ICA)
Independent component analysis separates a multivariate signal into additive subcomponents that are maximally independent. Unlike PCA, ICA will give produce statistically independent components. For ICA, as we get the different answer for different number of components, I have calculated average kurtosis for each of the components to select the one with higher average kurtosis. There can be different metrics which can be used for analysis, like training an SVM and selecting the best number of components based on the classifier performance. But I selected Kurtosis as I did not want to add any algorithm bias for analysis. 
For the Wine data (set 1), I have plotted the first two features of the ICA analysis result to study clusters of different sizes on the Wine dataset as shown in Figure 5. It is seen that for component value 2, 3 proper clusters are noticed.  It is interesting to see how the dimensions are reduced and from there we can get a to proper understanding of the data. As these 3 clusters resembles that of the 3 wine types based on the chemical composition. When the component value = 3, the clusters start to merge with itself. This gets bad with the increase of components.
![ICA Wine Data](/assets/images/ml_assets/ml_ica_wine_data.png)


But it is important to note that this plot is only with the independent analysis of 1st and 2nd component. An individual component analysis for larger component values may also give more insight for the data. From the average kurtosis values, plotted for component sizes, it is seen that it is lowest for 2 components. 
For the mushroom data (2nd dataset), similarly I can see the best clusters are seen when component value is 3 as shown in figure 6. The mushroom data shows here 2 clusters because I am plotting there with the Y label which contains only edible and poisonous categories. Because of that the clusters might not be so prominent as that of the wine dataset. From the kurtosis graph shows lowest kurtosis for 3 as component value.
![ICA Mushroom](/assets/images/ml_assets/ml_ica_mushroom_data.png)