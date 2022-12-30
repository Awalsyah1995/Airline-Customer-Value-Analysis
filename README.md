# <center> K-Means CLustering: Airline-Customer-Value-Analysis </center>
The goal of this project is to divide airline customers into segments and to make business recommendation from the clustering model. The model itself will be built based on LRFMC anaylis that have been used in aviation industry to analyze customer value.

RFMC analysis consists of 5 aspects:
- L : The number of months since the member’s joining time from the end of the observation time. => LOAD_DATE - FFP_DATE
- R : Number of months since the member’s last flight from the end of observation time. => LAST_TO_END
- F : The total number of times the member has flown during the observation period. => FLIGHT_COUNT
- M : Miles accumulated during member observation time. => SEG_KM_SUM
- C : The average value of the discount factor used by the member during the observation period. => avg_discount

## 1. Exploratory Data Analysis (EDA)
### A. Descriptive analysis
1. The dataset consists of 5 categorical columns and 18 numerical columns.
2. Missing values found in feature: Age, Revenue (SUM_YR_1, SUM_YR_2), WORK_CITY, WORK_PROVINCE, WORK_COUNTRY.
3. 0 duplicate rows found.

### B. Univariate Analysis
1. Most of the features have outliers and right-skew distribution.
2. Most of the customers are 26-60 years old.
3. Discount feature has some strange values, there are some rows with discount above 100%.
4. Age has strange maximum values, there is someone 110 years old.

## 2. Data Pre-Processing
1. Missing values handling:
- age columns are filled by median value.
- Revenue (SUM_YR_1 & SUM_YR_2) are filled by 0.
- WORK_CITY, WORK_PROVINCE, and WORK_COUNTRY are dropped because they have too many unique values.
2. Remove outlier with z-score
3. Feature Engineering
Select 5 feature from dataset that will be used for LRFMC analysis:
- L : The number of months since the member’s joining time from the end of the observation time. => LOAD_DATE - FFP_DATE
- R : Number of months since the member’s last flight from the end of observation time. => LAST_TO_END
- F : The total number of times the member has flown during the observation period. => FLIGHT_COUNT
- M : Miles accumulated during member observation time. => SEG_KM_SUM
- C : The average value of the discount factor used by the member during the observation period. => avg_discount

## 3. Modelling
- Clustering model algorthm: K-Means Clustering
- Number of clusters after practicing Elbow Method: 4.
- Visualize the cluster model with PCA
![cluster](https://user-images.githubusercontent.com/116500936/210029332-852958a7-e719-4d3e-a6d7-1e345d0b2e8d.png)

## 4. Analysis
Cluster summary statistic:

![stat](https://user-images.githubusercontent.com/116500936/210029143-b7c408f7-cc4b-4e65-875f-1e3161886c6d.png)

Cluster statistic boxplot visualization:

![boxplot](https://user-images.githubusercontent.com/116500936/210029312-d11667b2-b4ec-42e3-8e6a-459304f94cb8.png)


Cluster characteristics:
1. Cluster 0 (The Most Loyal Customer)
- The 2nd oldest member
- The shortest recency
- The highest flying frequency
- The highest flying distance

2. Cluster 1 (New Customer but Fly Often)
- The newest member.
- The 2nd recency, mostly have flight in recent time.
- Medium flying count.
- Medium flying distance.

3. Cluster 2 (Potential Churned Customer)
- The second newest member.
- Havent’t flight recently (> 1 year).
- Lowest flight frequency.
- Lowest miles/distance accumulated.

4. Cluster 3 (Casual Customer)
- The oldest member.
- Recency, Frequency, and flying distance are almost identic with cluster 1.

## 5. Business Recommendation
1. Create loyalty membership based on this clustering.
Example:
- Gold: Cluster 0.
- Silver: Cluster 1 and 3.
- Bronze: Cluster 2.
2. Avoid churned customer by give special treatment to cluster 2 customer:
- Push notification.
- Give Special promotion if they install airline apps or book flight for the first time since long time ago.
- Give local flight discount (considering their lowest distance accumulated).
3. Since cluster 1 customer are relatively new members but have flight in recent time, to engage them to become loyal customers by getting more flights, suggest them discount voucher/bundling package purchase.

 

