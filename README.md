# Customer Segmentation and RFM Analysis

This project aims to analyze customer behavior by segmenting them based on their Recency, Frequency, and Monetary (RFM) values. The segmentation is achieved through the application of clustering techniques like K-Means and Gaussian Mixture Models (GMM). The goal is to understand customer patterns and tailor marketing strategies accordingly.

### Key Objectives:
- **Targeted Marketing Campaigns**: Develop campaigns aimed at specific customer segments.
- **Customer Behavior Understanding**: Improve understanding of customer purchase patterns.
- **Resource Optimization**: Focus resources on the most valuable customer segments.

---

### Project Workflow:

1. **Data Preparation**:
   - Creating three separate DataFrames from CSV files: Customer, Product, and Order Data.
   - Integration of SQLite database for more structured data handling.
   - Data merging processes to create a unified dataset for analysis.

2. **Data Processing**:
   - Handling outliers using quantile methods (97% threshold).
   - Scaling the data with StandardScaler for better model performance.
   - Applying K-Means clustering and Gaussian Mixture Models to identify customer segments.

3. **Visualization**:
   - Visualizing the customer segments through scatter plots and bar charts for better insights.
   - Plotting average recency, frequency, and monetary values for each customer segment.

4. **Model Evaluation**:
   - Evaluating the models using Silhouette Score to assess the quality of clusters.
   - Refining the number of clusters and adjusting model parameters for optimal segmentation.

### Code Example:

```python
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import silhouette_score

# Prepare data for clustering
x = rfm[['Recency', 'Frequency', 'Monetary']]
scaler = StandardScaler()
x_scaled = scaler.fit_transform(x)

# Evaluate different cluster counts
wcss = []
ss = []
for i in range(2, 10):
    model = KMeans(n_clusters=i, random_state=42, n_init=10)
    model.fit(x_scaled)
    predictions = model.predict(x_scaled)
    ss.append(silhouette_score(x_scaled, predictions))

# Visualize results
plt.figure(figsize=(8, 5))
plt.scatter(rfm['Recency'], rfm['Monetary'], c=rfm['GMM_Segment'], cmap='viridis', s=50)
plt.title('Customer Segmentation')
plt.xlabel('Recency')
plt.ylabel('Monetary')
plt.show()
