# Examining Popularity with Clustering

We will use unsupervised learning to group tracks by the features that carry the most influence over their popularity and then examine how the popularity changes based on those descriptors.

Notebooks: 

[001_clustering_mehtod_selection](/001_clustering_mehtod_selection.ipynb)

[002_clustering_popularity_analysis](/002_clustering_popularity_analysis.ipynb)

## Experimental Design
In [EDA 5. Feature Selection](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/notebooks/EDA/EDA_Final.ipynb) we have concluded that the 4 most important features relating to popularity are:

```instrumentalness```, ```acousticness```, ```danceability``` and ```energy```.

The experiment will follow the process:
1. We examine how the key features relate to one another to see if they form any intuitive **clusters**.
2. We then apply a selection of appropriate clustering algorithms.

    2.1. We evaluate the performance of each algorithm using [the intrinsic measures](https://scikit-learn.org/stable/modules/clustering.html#clustering-performance-evaluation), provided by ScKitLearn[^1].
4. After fitting to the best performing model we compare the mean track audio features in each cluster to form **meaningful categories**.
5. Finally, we analyse the ```popularity``` measure within each category.

## Selecting Clustering Algorithms 
### Raw Data Analysis 
Before we select our model we will have a glance at the raw data, as not only the number of samples and type of data plays part in the selection of methods for clustering, but also the number and geometry of potential clusters to be discovered. 

<img src="/assets/4_key_feats_kde_plots.png" alt="Raw Data KDE Plots" width="650"/>

We can see that every single one of the key features is heavily concetrated around a single value (with the exception of ```instrumentalness```, which is bimodal). That means that the tracks are usually:
- (```acousticness```)......... Not acoustic
- (```instrumentalness```).. Fairly well split between lyrical and instrumental
- (```danceability```)......... Very fit for dancing (in terms of tempo, rhythm, beat)
- (```energy```)................... Very high energy (intense, fast, noisy, loud)

As evident from the scatter plots below, no intuitive clusters can be found. The data is rather homogenous.
<img src="/assets/4_key_feats_scatter_plots.png" alt="Raw Data Scatter Plots" width="650"/>

### Selecting The Algorithm

When selecting our approach we our primary concern is the computational complexities of the available methods, as our dataset is rather large, ```n~450k```. Here is a summary derived from [DATA MINING AND MACHINE LEARNING](https://dataminingbook.info/book_html/) by MOHAMMED J. ZAKI and WAGNER MEIRA, JR. and ScKitLearn[^2]:

### Table 1. Algorithm Complexity Summary
|Algorithm                   | Complexity                                                                            | Scalability |
|----------------------------|---------------------------------------------------------------------------------------|--------------------------------------------|
| **K-means**                | *O(tnkd)*                                                                             |**Very large** n_samples, medium n_clusters with MiniBatch code |
| MiniBatchKMeans            | The MiniBatchKMeans is a variant of the KMeans algorithm which uses subsets of the input data to reduce the computation time, while still attempting to optimise the same objective function.In contrast to other algorithms that reduce the convergence time of k-means, mini-batch k-means produces results that are generally only slightly worse than the standard algorithm. |
| Kernel K-means             | *O(tn<sup>2</sup>)*                                                                   |
| **Bisecting K-means**      | *O(tn(k-1)d)*                                                                         |**Very large** n_samples, medium n_clusters |
| K-Medoids                  | O(n<sup>2</sup>kt)                                                                    |
| _Expectation-Max*_         | *O(t(kd<sup>3</sup>+nkd<sup>2</sup>))* OR *O(tnkd)**                                  | potentially **Very large** n_samples |
| Agglomerative Hierarchical | *O(n<sup>2</sup>log(n))*                                                              |Large n_samples and n_clusters |
| **DBSCAN**                 | *O(nlog(n))* with a spatial index structure OR at most *O(n<sup>2</sup>)*             |**Very large** n_samples, medium n_clusters |
| Spectral Clustering        | at least *O(n<sup>2</sup>)* + *O(tnk<sup>2</sup>)*                                    |Medium n_samples, small n_clusters|
| Mean-Shift                 | *O(tnlog(n))* to *O(tn<sup>2</sup>)*                                                  |Not scalable with n_samples|
| Affinity Propagation       | *O(tn<sup>2</sup>)*                                                                   |Not scalable with n_samples|
| Ward                       | see Agglomerative Hierarchical                                                        |Large n_samples and n_clusters |
| OPTICS                     | see **DBSCAN**                                                                        |**Very large** n_samples, large n_clusters|
| **BIRCH**                  | It is a memory-efficient, online-learning algorithm provided as an alternative to MiniBatchKMeans. It constructs a tree data structure with the cluster centroids being read off the leaf. These can be either the final cluster centroids or can be provided as input to another clustering algorithm such as AgglomerativeClustering. | Large n_clusters and n_samples|
| CLARA                      | CLARA is related to the KMedoids algorithm. CLARA (Clustering for Large Applications) extends k-medoids to be more scalable, uses a sampling approach. | 
| Gaussian Mixture           |  is a probabilistic model that combines Expectation-Max with an init method (k-means, k-means++ or random) | Not scalable|

_*Expectation-Max_ can be used with a diagonal covariance matrix.

We need an algorithm that covers the following criteria:
<details><summary>is suitable  for a very large number of samples;</summary> Scales linearly;</details>
<details>
<summary>is suitable  for clustering with k<9; </summary> We are expecting the key features to be either:
<details>
<summary>1. acoustic- low</summary>
<details>
<summary>2. instrumentalness- low or high</summary>
<details>
<summary>3. danceability- mid or high</summary>
<details>
<summary>4. energy- mid or high</summary>
So, k <= 1x2x2x2 = 8.
</details>
</details>
</details>
</details>
</details>
<details><summary>is inductive. </summary> We do not know the number of clusters.</details>

## Model Fitting

Based on the criterea mentioned above, we select the following algorithms: **K-means, Bisecting K-means, BIRCH** and **DBSCAN**
### K-Means Clustering
We first look into **K-means** and **Bisecting  K-means**, which is a variant of it using divisive hierarchical clustering. To find the optimal number of clusters we will run the algorithm iteratively  with 1<k<15. Then using the inertia (the sum of squared distances of samples to their closest cluster center) and the elbow method we will find the best value for k.

<img src="/assets/k-means_elbow.png" alt="K-means Inertia" width="650"/>

We know that the performance is affected by the initialization of the cetnroids, so we will see if there is change if the centroids are allocated with the default initialization of ```init='k-means++'``` or with a random ones.

```
k-means++ centroids
Step 0: Cluster size: [284033  26448 140844] 
Davies Bouldin Score: 0.8167596563460061 
Calin Harab Score: 414807.4460555022

Step 1: Cluster size: [284033  26448 140844] 
Davies Bouldin Score: 0.8167596563460061 
Calin Harab Score: 414807.4460555022

Step 2: Cluster size: [284033  26448 140844] 
Davies Bouldin Score: 0.8167596563460061 
Calin Harab Score: 414807.4460555022

```
```
Random centroids:
Step 0: Cluster size: [ 26384 284081 140860] 
Davies Bouldin Score: 0.8160444113011217 
Calin Harab Score: 414807.7686065725

Step 1: Cluster size: [ 26384 284081 140860] 
Davies Bouldin Score: 0.8160444113011217 
Calin Harab Score: 414807.7686065725

Step 2: Cluster size: [ 26384 284081 140860] 
Davies Bouldin Score: 0.8160444113011217 
Calin Harab Score: 414807.7686065725
```
The random centroid allocation performs ever-so-slightly better, but in practice the difference is negligible. We can now evaluate the Silhouette Score[^3] (see Performance Evaluation table below).

We repeat the process for **Bisecting K-means.** Since this is a variant of K-means we expect the optimal number of k to be 3. When using **Bisecting K-means** we have the choice of two strategies: _"Biggest Inertia"_ vs _"Largest Cluster"_, i.e. precision vs speed. As speed is not an issue in our case, we will leave the strategy to the default setting of "Biggest Inertia" and see if this variant is performing better than it's original (see table below). 

<img src="/assets/k-means_vs_bisecting_elbow.png" alt="K-means Inertia" width="650"/>

### Table 2. Original vs Bisecting K-means Performance Evaluation
|Method                      | Silhouette Coefficient | Davies Bouldin Score                                                | Calinski-Harabasz Index |
|--------------------------|------------------|---------------------------------------------------------------------------|-------------------|
|                          | -1: incorrect clustering; +1: highly dense clustering; Around zero: overlapping clusters.| 0: the lowest possible score, indicates the best partition.| a higher value means better defined clusters| 
|**K-means**               | 0.5396586367325595 | 0.8160444113011217 | 414807.7686065725 |
|**Bisecting K-means**     | 0.5297647189181659 | 0.7879937835088743 | 396726.5725 |

We can see that K-means performs better in 2 out of 3 metrics. Moreover, the _Davies Bouldin Score_, which measures how well-separated the clusters are, is high to begin with, which is expected given the homogeneity of the data.

### Density Based Clustering
It could be possible that there are areas within the continous shape that have higher density than others, so we employ a density-based method, i.e. **DBSCAN** to examine this. As seen from [Table 1.](#table-1-algorithm-complexity-summary) the complexity of **DBSCAN** could be *O(n<sup>2</sup>)* at its worst. Indeed, in initial testing the run was taking several hours to complete. To tackle this we use the **BIRCH** algorithm to compress the input and then we use the _Clustering Feature Tree_ as an input for the **DBSCAN.** Another thing to note is that **DBSCAN** is a transductive algorithm so we need to select a value for k.

#### BIRCH Tuning
**BIRCH** can be used for both supervised and unsupervised learning. It creates a tree called a _Clustering Feature Tree_ which holds the necessary information for clustering and is very memory efficient. The two main parameters are ```treshhold``` and ```branching_factor``` which control the splitting of the tree. We want to find the parameters where the number of clusters is ```3<k<9```. We first test for different values of the ```threshhold```.

```
Threshold Tuning:
Start: 2023-11-21T19:51:12 threshold: 0.5
End: 2023-11-21T19:53:07, clusters: None, subclusters: 1

Start: 2023-11-21T19:51:12 threshold: 0.45
End: 2023-11-21T19:53:17, clusters: None, subclusters: 2

Start: 2023-11-21T19:51:12 threshold: 0.4
End: 2023-11-21T19:53:26, clusters: None, subclusters: 2

Start: 2023-11-21T19:51:12 threshold: 0.35
End: 2023-11-21T19:53:35, clusters: None, subclusters: 8

Start: 2023-11-21T19:51:12 threshold: 0.3
End: 2023-11-21T19:53:44, clusters: None, subclusters: 23

```
We can see that the optimal ```threshold``` is between 0.4 and 0.3. We refine our tuning.
```
Threshold Fine Tuning:
Start: 2023-11-21T20:04:19 threshold: 0.37
End: 2023-11-21T20:04:56, clusters: None, subclusters: 2

Start: 2023-11-21T20:04:19 threshold: 0.36
End: 2023-11-21T20:05:06, clusters: None, subclusters: 7

Start: 2023-11-21T20:04:19 threshold: 0.35
End: 2023-11-21T20:05:15, clusters: None, subclusters: 8

Start: 2023-11-21T20:04:19 threshold: 0.34
End: 2023-11-21T20:05:25, clusters: None, subclusters: 9
```
We select 0.36 as it is the highest possible value of the threshold. As we are keeping the number of (sub)clusters low the ```branching_factor``` does not have any effect on performance. The evaluation of the supervised run is in [Table 3.](#table-3-final-performance-evaluation)

#### DBSCAN Clustering
We can now run **BIRCH** with ```n_clusters``` set to an instance of **DBSCAN**, to perform clustering and see how it compares to K-means. The most important parameter for **DBSCAN** is ```eps``` which is effectively the measure of density. We iteratively try to find the best value.
```
Start: 2023-11-21T23:54:11 eps: 0.65
End: 2023-11-21T23:54:20, clusters: [0 1], Davies Bouldin Score: 0.7724428013806582, Calin Harab Score: 483751.62101898994

Start: 2023-11-21T23:54:20 eps: 0.6
End: 2023-11-21T23:54:30, clusters: [0 1], Davies Bouldin Score: 0.7724428013806582, Calin Harab Score: 483751.62101898994

Start: 2023-11-21T23:54:30 eps: 0.55
End: 2023-11-21T23:54:39, clusters: [-1  0  1], Davies Bouldin Score: 0.8858288569933866, Calin Harab Score: 362764.64210314606

Start: 2023-11-21T23:54:39 eps: 0.5
End: 2023-11-21T23:54:49, clusters: [-1  0  1], Davies Bouldin Score: 0.8858288569933866, Calin Harab Score: 362764.64210314606

Start: 2023-11-21T23:54:49 eps: 0.45
End: 2023-11-21T23:54:58, clusters: [-1  0  1], Davies Bouldin Score: 0.9997858748114062, Calin Harab Score: 381411.5033569091

Start: 2023-11-21T23:54:58 eps: 0.4
End: 2023-11-21T23:55:08, clusters: [-1  0  1], Davies Bouldin Score: 0.9997858748114062, Calin Harab Score: 381411.5033569091
```
We know that the _Calinski-Harabasz Index_ is generally lower for clusters obtained with **DBSCAN**, so we focus on the _Davies Bouldin Index(DBI)_. We can see that when ```eps``` is going towards ```0.0```, the _DBI_ is going up. Samples labelled as ```-1``` are considered noise. Therefore the best value for ```eps``` is ```0.7```. Since the **K-means** clustering indicated that there are 3 clusters, we could investigate how the noise is distributed and if it is forming a cluster of its own.

Another approach for selecting the right value of ```eps``` is measuring the actual distance between points using **NearestNeighbours** and the elbow method, however when attempted the suggested ```eps``` was ```0.0345``` (as the raw data is very homogenous) which does perform any clustering at all.

## Clustering Method Evaluation and Conclusion
### Table 3. Final Performance Evaluation
|Method                    |Number of clusters |Silhouette Coefficient   | Davies Bouldin Index | Scaled Calinski-Harabasz Index | Overall Score |
|--------------------------|-------------------|--------------------------|---------------------|--------------------------------|-----|
|                          | k |-1: incorrect clustering; +1: highly dense clustering; Around zero: overlapping clusters.| 0: the lowest possible score, indicates the best partition.| a higher value means better defined clusters|
|**K-means**               | 3 |0.5396586367325595  | 0.8167596563460061  | 0.41480777   | 0.38  |
|**Bisecting K-means**     | 3 |0.5297647189181659  | 0.7879937835088743  | 0.39672657   | 0.38 |
|**BIRCH**                 | 7 |0.31059723173761006 | 0.8858288569933866  | 0.3814115   | 0.14 |
|**DBSCAN**, ```eps=0.55```| 3 |0.5288451563463018  | 0.8858288569933866  | 0.3814115    | 0.30 |
|**DBSCAN**, ```eps=0.7``` | 2 |0.518989100877699   | 0.7724428013806582   |  0.48375162   | 0.41 |

The average of the three scores is taken, after the _CHI_ is scaled down by a factor of 1 000 000 and the _DBI_ is substracted from 1 as 0 is the best score. Altough **DBSCAN** has the highest average score, it only produced two clusters, based on accousticness, which upon examination show the same distribution of popularity. So in practice, we can see that the best performing method is **K-means.**

## Popularity Analysis Within Each Cluster

We apply our best performing clustering models to divide the data into categories, we can visualise using the same scatter plots as the ones used in the raw data analysis.

<img src="/assets/4_key_feats_clustered_scatter_plots.png" alt="Raw Data Scatter Plots" width="650"/>

We note the sizes of the clusters: 
```
0     26384 - small
1    284081 - big
2    140860 - medium
```

### Cluster Analysis
Using radar plots we can get a better understanding of what the categories are. We define labels for the clusters and add them to the raw dataset to investigate how they are relating to the popularity of tracks. The labels are as follows:

**Balanced Relaxing** - (vis. in purple) has mid danceability and energy, high acousticness and instrumentalness. 

**Party Instrumental** - (vis. in teal) that has an average high instrumentalness, danceability and energy. We note that it has essentially no acousticness.

**Party Lyrical** - (vis. in yellow) has high energy and danceability, but essentially no acousticness and instrumentalness.  

![clustered radar plots](/assets/k-means_radar_plots.png)
![clustered pie chart](/assets/k-means_pie_chart.png)

Finally we investigate the popularity within each cluster. As the data is heavily skewed we will have a look at the IQR as well.

![clustered popularity histogram](/assets/populaity_in_k-means_clusters_hist.png)
![clustered popularity IQR histogram](/assets/populaity_in_k-means_clusters_IQR_hist.png)

The mean popularity in each category is: 
```
Party Lyrical Mean Popularity:      7.910419974812462
Party Instrumental Mean Popularity: 4.905751311391957
Balanced Relaxing Mean Popularity:  7.2391912147724495
```

The same proccess was applied to **DBSCAN**, resulting in two less-defined categories absorbing the balanced acoustic tracks. No difference in popularity is observed. (see end of notebook [002_clustering_popularity_analysis](002_clustering_popularity_analysis.ipynb))

![clustered radar plots](/assets/dbscan_radar_plots.png)
![clustered popularity IQR histogram](/assets/populaity_in_dbscan_clusters_IQR_hist.png)

### Cluster Analysis Conclusion
We can see that tracks that are lyrical are more likely to be popular than tracks that are not. Lyrical tracks with high energy/danceability are slightly more popular than the minorty of balanced ones present in the data.

## Limitations and applicability
When considering the results of the clustering experiment one should keep in mind the composition of the raw data. As seen in the exploratory stage as well as when looking for an optimal value for the distance between data points, the data is extremely homogeneous, so the clustering itself is not very substantial. This comes from the fact that the dataset consists of mainly electronic music, i.e. a single genre and the features describing the tracks are too general to capture the nuances between sub-genres. Perhaps, a similar genre-specific experiment could be conducted using more technical-specific data in terms of audio features. Or, if the data spans over several genres, the same experiment could produce more meaningful results.

[^1]: 2.3.11. Clustering performance evaluation; See 2.11.5-6-7
[^2]: 2.3.1. [Overview of clustering methods.](https://scikit-learn.org/stable/modules/clustering.html#k-means)
[^3]: We do this last as it proved to be slow, around 40 min per call.


