# Customer Segmentation with K-Means Clustering

## Overview
This Jupyter Notebook implements a customer segmentation pipeline using K-Means clustering on the “Mall Customers” dataset. The goal is to group customers into distinct clusters based on their annual income and spending score, enabling marketing teams to tailor campaigns to each segment.

## Dataset
- **Source**: Kaggle’s “Mall Customers” dataset  
- **File**: `Mall_Customers.csv`  
- **Description**: Each record represents a customer and contains the following columns:
  - `CustomerID`: Unique identifier for the customer
  - `Gender`: Male/Female
  - `Age`: Customer’s age
  - `Annual Income (k$)`: Annual income in thousands of dollars
  - `Spending Score (1–100)`: A metric assigned by the mall based on customer behavior and spending patterns

# What’s Implemented

This section outlines the core functionality and processing steps implemented in the notebook:

- **Data Loading**
  - Read the “Mall_Customers.csv” file into a Pandas DataFrame.
  - Verified successful loading by inspecting head/tail rows and DataFrame shape.

- **Initial Data Inspection**
  - Displayed basic information (`.info()`, `.describe()`) to check data types and identify missing values.
  - Confirmed no null entries and understood column distributions.

- **Exploratory Data Analysis (EDA)**
  - Generated a histogram of `Age` to visualize the age distribution of customers.
  - Created a scatter plot of `Annual Income (k$)` vs. `Spending Score (1–100)`, color-coded by `Gender`, to observe potential grouping patterns.

- **Feature Extraction for Clustering**
  - Selected two numeric features—`Annual Income (k$)` and `Spending Score (1–100)`—and constructed a NumPy array `X` containing these columns.

- **Elbow Method to Determine Optimal \(k\)**
  - Iterated \(k\) from 1 to 10:
    - Instantiated `KMeans(n_clusters=k, init='k-means++', random_state=0)`.
    - Fitted the model on `X` and recorded the within-cluster sum of squares (WCSS) via `inertia_`.
  - Plotted the WCSS values against \(k\) to identify the “elbow” point (around \(k=5\)).

- **K-Means Clustering (with \(k=5\))**
  - Created a `KMeans` object with `n_clusters=5` and fitted it to the feature matrix `X`.
  - Obtained cluster labels (`labels`) for all data points using `.fit_predict(X)`.

- **Cluster Visualization**
  - Produced a 2D scatter plot of the two chosen features, assigning a distinct color to each of the 5 clusters:
    - Iterated through each cluster index, plotted points where `labels == i`.
  - Overlaid cluster centroids as large “X” markers in cyan, using `kmeans.cluster_centers_`.

- **Final Outcome**
  - Clearly separated 5 customer segments in the “Annual Income vs. Spending Score” space.
  - Marked centroids to visualize the “center” of each segment.
 
# Outcomes

This section summarizes the key results produced by the notebook’s customer-segmentation pipeline:

- **Elbow Method Plot**  
  - A line chart of Within-Cluster Sum of Squares (WCSS) vs. number of clusters (k = 1–10).  
  - The “elbow” appears at **k = 5**, indicating that five clusters capture most of the variance without overfitting.  

- **Final Cluster Assignments**  
  - Using K-Means with **n_clusters = 5**, every customer is assigned a label (1 through 5).  
  - The cluster labels divide the customer base into five distinct segments in the 2D space of **Annual Income (k$)** vs. **Spending Score (1–100)**.  

- **Cluster Centroids**  
  - Each of the 5 centroids represents the “average” customer in that segment (centered on income & spending score).  
  - These centroids can be used as reference points for campaign targeting:
    1. **Cluster 1 Centroid:** (High Income, High Spending)  
    2. **Cluster 2 Centroid:** (Low Income, Low Spending)  
    3. **Cluster 3 Centroid:** (High Income, Low Spending)  
    4. **Cluster 4 Centroid:** (Medium Income, Medium Spending)  
    5. **Cluster 5 Centroid:** (Low–Medium Income, High Spending)  
  - *(Note: exact numerical coordinates will vary slightly depending on the dataset version. In the deployed notebook, these values are computed automatically and displayed on the final plot.)*

- **Cluster Size Distribution**  
  - The notebook calculates and prints how many customers fall into each of the 5 clusters (e.g., 23 in Cluster 1, 20 in Cluster 2, etc.).  
  - This count helps identify which segments are the largest (priority for marketing budgets) or smallest (niche audiences).  

- **Cluster Visualization**  
  - A 2D scatter plot displays all customers colored by their assigned cluster (five distinct colors).  
  - Centroids are overlaid as large “X” markers in cyan.  
  - This visualization confirms that:  
    - **Cluster 1** (e.g., “High Income, High Spending”) is clearly separated in the upper-right quadrant.  
    - **Cluster 2** (e.g., “Low Income, Low Spending”) appears in the lower-left.  
    - **Cluster 3** (“High Income, Low Spending”) lies along the top-left.  
    - **Cluster 4** (“Medium Income, Medium Spending”) occupies the center region.  
    - **Cluster 5** (“Low–Medium Income, High Spending”) is in the lower-right.  

- **Business Insights**  
  - **Cluster 1 (High Income, High Spending):**  
    - Ideal target for premium or loyalty programs.  
    - Likely to respond to exclusive offers, upscale products, and VIP events.
  - **Cluster 2 (Low Income, Low Spending):**  
    - Cost-conscious customers.  
    - May respond to discounts, bundle deals, and entry-level products.
  - **Cluster 3 (High Income, Low Spending):**  
    - Potential to increase spending if engaged with the right messaging.  
    - Consider personalized upsell or luxury offers to drive conversion.
  - **Cluster 4 (Medium Income, Medium Spending):**  
    - Core customer base with moderate budget and moderate engagement.  
    - Responsive to seasonal promotions and mid-tier product lines.
  - **Cluster 5 (Low–Medium Income, High Spending):**  
    - Value-driven yet willing to spend (e.g., bargain hunters or trend-focused).  
    - Effective targets for value packs, flash sales, or limited-time offers.

- **Reproducibility**  
  - All plots and computed values (WCSS, centroids, labels) are generated automatically when running the notebook cells in sequence.  
  - If the dataset is updated or enlarged, re-running the notebook will recalculate these outcomes and adjust cluster assignments accordingly.

---

> **Note:** The exact numeric coordinates of centroids and cluster sizes depend on the specific “Mall Customers” dataset version used. To view the precise values, refer to the final code cells in the notebook, which print or plot those metrics directly.  

