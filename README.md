# Cluster-Analysis-in-R
The main goal of this project was to determine which variables are important in creating clusters for cluster analysis, and then using hierarchical or k-means clustering to group the brands of cigarettes into optimal clusters. Further, it was required that the cigarette brands be ranked on their level of harmfulness.

# Factor Analysis and Dimensionality Reduction
From the initial correlation heat map as shown above, except Price and Weight, all other variables, CO, Nicotine and Tar are highly correlated, indicating multicollinearity. Therefore, to select the most important variable/variables from these three(CO, Nicotine and Tar), Principal Component Analysis(PCA) and external research was performed.
As can be seen from PCA plot, Nicotine, CO and Tar are positively correlated with each other, hence are grouped together. 
From the scree plot , the first three principal components explain 98.2% of the variance in the data, hence three dimensions are sufficient to explain variation in data.
              Dim.1       Dim.2     Dim.3      Dim.4       Dim.5
Tar      29.6291961  0.11367741  4.363031  3.6208772 62.27321841
Nicotine 29.2986292  0.69132323  2.054308 36.5291627 31.42657726
Weight   12.3220820 14.61025040 72.818503  0.2353117  0.01385256
CO       28.3461762  0.05410862  6.195751 59.2261156  6.17784897
Price     0.4039165 84.53064033 14.568408  0.3885328  0.10850279

Since it was concluded that three dimensions were enough to explain most of the variance in the data, the contribution of variables to these three dimensions were examined. The table above shows the contribution of each variable to each dimension or principal component. In Dimension 1, Tar has the highest contribution. In Dimension 2, Price has the highest contribution and in Dimension 3, Weight has the highest contribution. 
Therefore, the final set of variables selected is: Price, Weight and Tar.

# Building the Cluster Model
## Data Preparation:
In this step, the following checks were performed:
-	Missing values
-	Incorrect data type
  o	Price was stored in the data set with ‘$’ sign, hence this needed to be converted to numeric format.
-	Scaling the data
  o	This was necessary as clustering algorithms tend to depend on variables that have larger magnitudes. Therefore, to avoid this from happening, the variables were scaled.
## Choice of Clustering algorithm
There are two algorithms that were considered, Hierarchical and K-means clustering. To decide the best algorithm for this purpose, the following were considered:
1.	Size of the dataset
2.	Knowledge of number of clusters apriori
3.	Reproducibility of the algorithm
4.	Presence of outliers
With all the above factors in mind, the k-means clustering algorithm was finally selected. It was noteworthy that both algorithms produced similar results. 
## Determining Optimal number of clusters
To determine the optimal number of clusters, the following methods were considered:
1.	Elbow Method
    From the "Elbow" plot, a distinct “elbow” cannot be seen. However, the “elbow” seems to occur at either k=5 or k=6.
    Therefore, two different clustering solutions will be created with k=5 and k=6
2.	Silhouette Method
    From the plot, the silhouette method suggests that the optimal number of clusters should be 9. Therefore, the third clustering         solution that was considered was with k=9.
## Selecting Best CLustering Model
To select the best clustering model, the "Within Sum of Squares (WSS)" and "Between sum of squares (BSS)" for each of the clustering solution was compared. 
From this comparison, model with k=9 has the least within group sum of squares and highest between group sum of squares. Additionally, the outlier, Bull Durham is correctly identified as an outlier.
Characteristic of each of the clusters in terms of tar content, weight of the cigarette and price are shown below:
 Cluster	Tar Content	Weight	Price
1	Low	      Low	              Low
2	High	    Low	              Medium
3	Medium	  Medium	          Low
4	High	    High	            Medium
5	Low	      Low	              High
6	Low	      Medium	          Medium
7	Medium	  Medium	          Medium
8	Medium	  Low	              High
9	Medium	  Medium 	          Low

# Business Insight & Recommendation
## Recommendation
To rank the dataset, the following steps were followed:
1.	First the 9 clusters were sorted by the cluster mean Tar content in ascending order
2.	Then within each of the ordered clusters, the brands were sorted by their tar content
For example, cluster 1 had the lowest mean tar content, and within this cluster, brands NOW and Newport Lights are ordered by the tar content. 
From this order of ranking, it can be recommended that the cigarette brand, "Bull Durham" is the most harmful, while the cigarette brand "NOW" is the least harmful. 
Brand	              Tar	  Nicotine	Weight	CO	Price	cluster
Now	                1.0	  0.13	    0.79	  1.5	  8.25	2
Newport Lights	    9.0	  0.74	    0.85	  9.5	  7.30	2
Carlton	            4.1	  0.40	    0.95	   5.4	16.25	7
Salem Ultra	        4.5	  0.42	    0.91	   4.9	14.00	7
Viceroy Rich Lights	8.6	  0.69	    0.97	  10.6	13.65	7
TRUE	              7.3	  0.61	    0.98	  8.5	  10.55	4
Merit	              7.8	  0.57	    0.97	  10.0	10.50	4
Golden Lights	      8.8	  0.76	    1.03	  9.0	  11.00	4
Camel Lights	      8.0	  0.67	    0.93	  10.2	18.25	5
Marlboro	          15.1	0.90	    0.93	  14.4	17.40	5
Multifilter	        11.4	0.78	    1.12	  10.2	9.30	1
Winston Lights	    12.0	0.82	    1.12	  14.9	12.30	1
Benson & Hedges	    16.0	1.06	    1.09	  16.6	12.40	1
Pall Mall Light	    12.8	1.08	    1.04	  12.6	5.50	6
Tareyton	          14.5	1.01	    1.01	  15.9	7.75	6
Kent	              12.4	0.95	    0.92	  12.3	10.50	8
Lark Lights	        13.7	1.01	    0.96	  13.0	8.65	8
L&M	                14.9	1.02	    0.89	  15.4	9.85	8
Chesterfield	      15.0	1.04	    0.89	  15.0	6.60	8
Virginia Slims	    15.2	1.02	    0.95	  13.9	8.00	8
Old Gold	          17.0	1.26	    0.92	  18.5	9.35	8
Alpine	            14.1	0.86	    0.99	  13.6	13.50	3
Raleigh	            15.8	0.96	    0.96	  17.5	11.25	3
Kool	              16.6	1.12	    0.94	  16.3	11.68	3
Bull Durham	        29.8	2.03	    1.17	  23.5	12.67	9
## Business Insight
Tar is the element that is responsible for most of the health risk, including certain types of cancer. Tar builds up in the lungs and can end up travelling through the blood stream to other organs leading to serious conditions such as heart diseases, diabetes, etc. Tar is also an element that does not get filtered by cigarette filters. Therefore, it is more harmful than the other elements. Additionally, since tar does not leave the body and gets deposited in a smoker’s lungs, therefore, it is an indicator of health risks. Therefore, to rank the brands from least harmful to most harmful, the brands were ranked on their level of tar content. "Now" brand of cigarettes has the lowest tar content. Coincidently enough, the CO and nicotine content is also low in this brand. This is probably driven by the fact that tar, nicotine and CO contents are highly correlated.


