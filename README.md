# Customer_segmentation

## About the dataset
Customer Personality Analysis is a detailed analysis of a company’s ideal customers. It helps a business to better understand its customers and to modify its product based on its target customers from different types of customer segments, accomodating to the specific needs, behaviors and concerns of different types of customers.

### Observations from missing values

- There is a small percentage of values missing from income. We can go ahead and drop those observations
- An other thing to note is that Dt_Customer is in the str datatype, and have to be parsed to DateTime
- Education and Marital_Status are in the str datatype as well, hence will have to be encoded into numeric datatypes

## Feature Engineering

- Creating a new feature to get a count of number of days since the customer is registered with the company
- Understanding the only two categorical features Marital_Status and Education
- Dropping few redundant features

## Handling Outliers

```sh
# Outlier handling
cust_data = cust_data[cust_data['Age']< 95]
cust_data = cust_data[cust_data['Income'] < 600000 ]
print('Total observations in dataset after handling missing values and outliers: ', len(cust_data))
```

## Pairplot and Correlation Matrix

![alt text](https://github.com/Dharssini/Customer_segmentation/blob/main/PairPlot.png)
![alt text](https://github.com/Dharssini/Customer_segmentation/blob/main/CorrelationMatrix.png)

### Observations:
- Income and Amount_Spent has the highest strong positive correlation
- Amount_Spent is strongly and positively correlated to Wine, Fruits, Meat, Fish, Sweets, Gold, since the aggregate amount of these items makes up the Amount_Spent feature
- Total_promos have a strong and positive correlation with AcceptedCmp features
- Amount_Spent is also strongly and positively correlated to NumWebPurchases, NumStorePurchases, NumCatalogPurchases, and Total_Promos

## Data Preprocessing
- Label Encoding for categorical features
- Scale features using StandardScaler (since we do not have too many outliers, use RobustScaler otherwise)
- Creating subset of dataset for dimensionality reduction

## Dimensionality Reduction

### Scree plot for PCA to find the optimal number of Principal Components from the dataset
![alt text](https://github.com/Dharssini/Customer_segmentation/blob/main/ScreePlot.png)

### Observation:
We see that there is a bend at index = 1, beyond which the variance explained decreases below 10%. But we take n_components = 3 so that the first 3 components contribute to about 54% of the total variation in the dataset
We set n_components = 3 for our Principal Component Analysis.

## Clustering and cluster Evaluation

### Tasks performed here:

- K-Means Clustering
- Optimum number of clusters using KElbowVisualizer for Elbow Method
- Optimum number of clusters using Silhouette Analysis
- Density-Based Spatial Clustering of Applications With Noise (DBSCAN)
- Plotting the clusters after DBSCAN in 3-D view
- Agglomerative Hierarchical Clustering
- Estimating similarity between clusters

#### Cluster evaluation

- Distribution of data points in clusters
- Scatterplot for 'Income' vs. 'Spending' of customers
- Boxenplots for visualizing the distribution of Amount_Spent by customers
- Analyzing past campaigns
- Boxenplot for Number of deals purchased
- Profiling

### Observations:

Cluster 0:

- Average Income, High Spending
- Are definitely a parent (also includes single parents)
- Most have two teenagers at home, or one teenager and one kid
- Either has a partner and kids, or is a single parent with kid
- Family size of 2 to 5
- Age span of 40 to 70
- Second most important set of customers

Cluster 1:

- High Income, High Spending
- Family size of 1 to 2, i.e. single and couples
- Mostly not a parent
- Spans across all age groups
- Biggest set of customers

Cluster 2:

- Average income, Low Spending
- Mostly not a parent, but some are with one kid (typically teenager)
- Mostly single
- Family size of 2 to 3
- Spans across all age groups

Cluster 3:

- Low income, Low Spending
- Mostly are a parent
- Mostly have two kids
- Most of them have partners
- Family size 3 to 5
- Age span of 30 to 60

