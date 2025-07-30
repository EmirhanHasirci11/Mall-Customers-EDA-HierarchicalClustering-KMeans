# Mall Customer Segmentation using EDA and Clustering

This project analyzes a dataset of mall customers to identify distinct segments based on their purchasing behavior. The primary goal is to perform Exploratory Data Analysis (EDA) to understand customer demographics and then apply unsupervised machine learning techniques—specifically **Hierarchical Clustering** and **K-Means Clustering**—to group customers into meaningful segments.

This segmentation can help the mall and its retailers to develop targeted marketing strategies.

## Dataset
[Kaggle](https://www.kaggle.com/code/emirhanhasrc/eda-hierarchicalclustering-kmeans?scriptVersionId=253216474)
The dataset contains basic information about mall customers, including their age, gender, annual income, and a "spending score" assigned by the mall based on their purchasing habits.

### Dataset Features

The dataset consists of 200 customer records and 5 features:

| Feature | Description | Type |
| :--- | :--- | :--- |
| **CustomerID** | A unique identifier for each customer. | Numeric |
| **Genre** | Gender of the customer. | Categorical (Male, Female) |
| **Age** | Age of the customer in years. | Numeric |
| **Annual Income (k$)**| Annual income of the customer in thousands of dollars. | Numeric |
| **Spending Score (1-100)** | A score assigned by the mall based on customer behavior and spending nature (1-100). | Numeric |

## Exploratory Data Analysis (EDA)

A detailed EDA was conducted to understand the data's characteristics and uncover initial patterns.

1.  **Initial Data Inspection**: The dataset was found to be complete and clean, with **no missing values**. The `CustomerID` column, being a unique identifier, was dropped as it provides no predictive value for clustering.
2.  **Feature Distributions**:
    -   **Histograms**: Distributions of numerical features (`Age`, `Annual Income`, `Spending Score`) were visualized. `Age` shows a fairly wide distribution, while `Annual Income` and `Spending Score` are centered around the middle of their ranges.
    -   **Gender Distribution**: A count plot revealed that the dataset contains more female customers (112) than male customers (88).

3.  **Relationship Analysis**:
    -   **Scatter Plot**: The relationship between `Annual Income` and `Spending Score` was visualized using a scatter plot. This plot clearly showed the potential for distinct clusters, forming the primary basis for the segmentation.

## Modeling - Customer Segmentation

Unsupervised clustering algorithms were used to segment the customers. The analysis focused on the two most relevant features for marketing: `Annual Income` and `Spending Score`.

### 1. Data Preprocessing

-   The `CustomerID` column was dropped.
-   The categorical `Genre` column was converted to numerical format using `LabelEncoder`.
-   All features were scaled using `MinMaxScaler` to ensure that no single feature dominates the clustering algorithms due to its scale.

### 2. Hierarchical Clustering

-   **Dendrogram**: A dendrogram was plotted using the **Ward linkage** method. This visualization helps in determining the optimal number of clusters by identifying the largest vertical distances that don't intersect any horizontal lines. The dendrogram suggested that **5 clusters** would be an appropriate choice for this dataset.
-   **Agglomerative Clustering**: An `AgglomerativeClustering` model with `n_clusters=5` was fitted to the data.
-   **Evaluation**: The silhouette score for the clustering was calculated to be approximately **0.55**, indicating a reasonably good clustering structure. The resulting clusters were visualized on a scatter plot.

### 3. K-Means Clustering

-   **Elbow Method**: To confirm the optimal number of clusters, the Elbow Method was employed. By plotting the Within-Cluster Sum of Squares (WCSS) for a range of k-values, the "elbow" point was identified at **k=5**, reinforcing the choice of 5 clusters.
-   **Model Fitting**: A `KMeans` model with `n_clusters=5` was trained on the data.
-   **Visualization**: The final clusters were visualized on a scatter plot of `Annual Income` vs. `Spending Score`, which clearly showed five distinct customer segments.

## Cluster Analysis - Customer Segments

Based on the K-Means clustering results, five distinct customer segments were identified:

1.  **Careful Customers** (Cluster 0):
    -   **Characteristics**: High annual income but low spending score.
    -   **Interpretation**: These customers earn well but are cautious with their spending. They might be targeted with high-quality, durable products or value-oriented promotions.

2.  **Standard Customers** (Cluster 1):
    -   **Characteristics**: Average annual income and average spending score.
    -   **Interpretation**: This is the largest segment, representing the typical mall customer. Standard marketing campaigns would be effective for this group.

3.  **Target Customers (VIPs)** (Cluster 2):
    -   **Characteristics**: High annual income and high spending score.
    -   **Interpretation**: This is the most valuable segment. They are prime candidates for premium offers, loyalty programs, and exclusive product previews.

4.  **Careless Customers** (Cluster 3):
    -   **Characteristics**: Low annual income but high spending score.
    -   **Interpretation**: These customers spend freely despite having lower incomes. They could be targeted with deals, discounts, and trendy, affordable products.

5.  **Sensible Customers** (Cluster 4):
    -   **Characteristics**: Low annual income and low spending score.
    -   **Interpretation**: This group is cautious and has limited purchasing power. They are likely to respond to essential items and deep discounts.

## Conclusion

The exploratory data analysis and subsequent clustering successfully identified five distinct and actionable customer segments within the mall's clientele. Both Hierarchical Clustering (guided by the dendrogram) and K-Means Clustering (guided by the Elbow Method) independently confirmed that **five clusters** provide the most meaningful segmentation.

These insights are highly valuable for the mall's marketing department. By understanding the different customer profiles, they can tailor their advertising, promotions, and product offerings to better meet the needs of each segment, ultimately driving sales and improving customer satisfaction.
