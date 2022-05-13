## Document Overview
This document showcases the implementation of k-means clustering algorithm that I used to cluster food products by its nutritional content. 


### Elbow Method
In order to identify the optimal number of clusters to be used in the analysis, elbow method was utilized. below code shows that for loop was used calculate and create a list of Within-Cluster-Sum-of-Squares. 
Line plot was also produced to identify the 'elbow'. From the line plot, it is appropriate to choose 3 for the elbow for this analysis.
```python
#To choose the riht number of k, perform an elbow method. 
wcss = []
for k in range(1, 7): 
    kmeans = cluster.KMeans(k)
    kmeans.fit(train_data1[['Cal/Gram','Prot/Gram']])
    wcss_iter = kmeans.inertia_
    wcss.append(wcss_iter)
plt.plot(range(1,7), wcss)
plt.title('The Elbow Graph')
plt.xlabel('# Clusters')
plt.ylabel('WCSS')
#We'll use 3 clusters
```
![Elbow](https://github.com/takucnoel-endo/Images/blob/K-means/Elbow.png)

### Clustering
Using the value of clusters was aqquired in the previous step, the clusters can be allocated for each data point. 
For this step, KMeans() method from sklearn.cluster was used to identify each cluster allocation. 3 centroids were also identified as shown below.
```python
#Create a model. 
km3 = cluster.KMeans(n_clusters = 3)
y_pred3 = km3.fit_predict(train_data1[['Cal/Gram','Prot/Gram']])
centroid = km3.cluster_centers_
print('Labels:')
print(y_pred3)
print()
print('Centroids:')
print(centroid)
```
![Output K-means](https://github.com/takucnoel-endo/Images/blob/K-means/Result%20output.png)


### Cluster Visualization
```python
sns.scatterplot(x = 'Cal/Gram', y = 'Prot/Gram', hue = 'Cluster', data = train_data1, alpha = 0.6)
sns.scatterplot(centroid[:, 0], centroid[:, 1], color = 'black', marker = '+')
```
![Vis K-means](https://github.com/takucnoel-endo/Images/blob/K-means/Result%202D.png)
