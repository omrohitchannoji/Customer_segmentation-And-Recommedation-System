# 🧠 Customer Segmentation and Recommendation System

## 📘 Overview
This project focuses on **customer segmentation** and **personalized product recommendations** using data-driven analytics. It applies **RFM analysis** (Recency, Frequency, Monetary) and **K-Means clustering** to group customers based on purchasing behavior, followed by a **recommendation engine** built using the **ALS (Alternating Least Squares)** algorithm.

The goal is to help businesses identify key customer segments, understand purchasing patterns, and deliver tailored product recommendations to enhance customer retention and sales.

---

## 📊 Key Features
- **Data Preprocessing & Cleaning**: Handled missing values, outliers, and normalization.
- **Exploratory Data Analysis (EDA)**: Insights on Recency, Frequency, and Monetary value distributions.
- **Customer Segmentation**: Implemented **K-Means clustering** to classify customers into distinct groups.
- **Dimensionality Reduction**: Used **PCA** for visualizing high-dimensional customer data.
- **Recommendation Engine**: Built with **ALS** for personalized product recommendations.
- **Data Visualization**: Plots created using **Matplotlib**, **Seaborn**, and **Plotly**.

---

## 🧰 Tech Stack
- **Languages:** Python  
- **Libraries:**  
  `pandas`, `numpy`, `matplotlib`, `seaborn`, `plotly`, `scikit-learn`, `scipy`, `yellowbrick`, `tabulate`
- **Machine Learning:**  
  - Clustering: `KMeans` (from `sklearn.cluster`)
  - Dimensionality Reduction: `PCA`
  - Recommender System: `ALS`

---

## 🗂 Dataset
**File:** `Data.csv`  
Contains transaction-level data including:
- `CustomerID`
- `InvoiceNo`
- `StockCode`
- `Quantity`
- `InvoiceDate`
- `UnitPrice`
- `Country`

The dataset is used to compute **RFM features** and derive customer segments.

---

## 🚀 Project Workflow
1. **Data Import and Cleaning**
   - Removed nulls and duplicates
   - Handled outliers in purchase amounts

2. **Feature Engineering**
   - Computed Recency, Frequency, and Monetary scores
   - Derived behavioral and product diversity metrics

3. **Customer Segmentation**
   - Applied **K-Means clustering**
   - Visualized clusters using **PCA**

4. **Recommendation Engine**
   - Built an **ALS**-based collaborative filtering model
   - Generated personalized product recommendations

5. **Visualization and Insights**
   - Cluster profiling and RFM distribution analysis
   - Plotted customer groups using 2D/3D scatter plots

---

## 📈 Results
- Customers segmented into distinct behavioral groups (e.g., “High-Value”, “Frequent Buyers”, “At-Risk”).
- Recommendation model able to predict personalized products based on historical interactions.
- Visual dashboards created for easy interpretation of clusters and customer patterns.

---

## 🧩 How to Run
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/Customer-Segmentation-Recommendation.git
   cd Customer-Segmentation-Recommendation

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the notebook**
   ```bash
   jupyter notebook "Customer_segmentation And Recommendation System.ipynb"
   ```

---

## 📁 Project Structure

```
Customer-Segmentation-and-Recommendation-System/
│
├── Customer_segmentation And Recommendation System.ipynb   # Main notebook
├── data/                                                   # Folder for dataset(s)
├── README.md                                               # Project documentation
└── requirements.txt                                        # Python dependencies
```

---
📚 Future Enhancements

Integrate a web dashboard (e.g., Streamlit) for real-time insights

Add more recommendation techniques (content-based, hybrid)

Include A/B testing for model validation

🏁 Author
## 👨‍💻 Author
**Om Channoji**  
Aspiring Data Analyst | Python | SQL | Power BI | Machine Learning

📧 *Feel free to connect on LinkedIn or explore my GitHub for more projects!*

---

⭐ **If you find this project useful, don’t forget to star this repository!**
