
# Customer Segmentation using K-Means & PCA

## 📌 Project Overview
This project performs **customer segmentation** using unsupervised machine learning techniques to identify distinct customer groups based on demographics, spending behavior, engagement, and promotion sensitivity.  
The goal is to derive **actionable customer personas** that can be leveraged for targeted marketing and business strategy.

---

## 📊 Dataset Description
The dataset contains customer-level information including demographics, spending behavior, engagement, and marketing response.  
Extensive feature engineering was applied to capture customer value, preferences, and sensitivity.

---

## 🧹 Data Preprocessing
- Date parsing and customer tenure calculation  
- Outlier handling using force-fitting (winsorization-style capping)  
- Feature scaling using StandardScaler  

---

## 🧠 Modeling Approach
- PCA for dimensionality reduction and visualization  
- K-Means clustering with **k = 4**  
- PCA-based clustering selected due to better silhouette score and stability  

---

## 🧩 Final Cluster Profiles
- **Cluster 0**: Moderate income, value-driven loyal customers  
- **Cluster 1**: High income, high spending premium customers  
- **Cluster 2**: Low income, low spending price-sensitive customers  
- **Cluster 3**: Deal-driven, high spending despite lower income  

---

## 📁 Outputs
- PCA loadings and explained variance  
- Cluster-level feature averages  
- Visual cluster profiling plots  

---

## 🛠️ Tech Stack
Python, Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn

---

## 👤 Author
Riya
