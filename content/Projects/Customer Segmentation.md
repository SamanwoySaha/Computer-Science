---
title: Customer Segmentation
draft: false
tags:
date: 25-Aug-2025
---


[Website](https://customer-segmentation-app1.streamlit.app/) | [Github](https://github.com/SamanwoySaha/Customer-Segmentation/) 

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)  ![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)  ![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Machine%20Learning-green.svg)  
## 📋 Project Overview
  
This project implements customer segmentation analysis using K-Means Clustering. The segmentation helps businesses understand their customer base better and develop targeted marketing strategies.

![customer-segmentation.png](https://i.postimg.cc/Wzfn5zxJ/customer-segmentation.png)

[Dataset](https://www.kaggle.com/datasets/vishakhdapat/customer-segmentation-clustering)

### 1. **Data Exploration & Pre-processing**
- Data quality assessment and cleaning
- Missing value treatment
- Feature engineering and selection
### 2. **Exploratory Data Analysis (EDA)**
- Statistical summary of customer data
- Distribution analysis of key features
- Correlation analysis between variables
- Visualization of customer patterns
### 3. **Feature Engineering**
- Customer lifetime value calculation
- Standardization and scaling  
### 4. **Clustering Analysis**
- **K-Means Clustering**: Primary segmentation method
- **Elbow Method**: Optimal cluster determination
## 📈 Visualizations
The notebook includes comprehensive visualizations:
- Customer distribution across segments
- Age Distribution
- Income Distribution
- Total Spending Distribution
- Income by Education Level
- Spending by Marital Status
- Correlation Matrix (Income, Age, Recency, Total Spending, Number of Web Purchases, Number of Store Purchases)
- Heatmap (Average Income by Education and Marital Status)
- Average Spending by Education
- Campaign Acceptance Rate by Marital Status
- Average Income by Age Group
- ELbow Method for Optimal Cluster Size
- Customer Segmentation (PCA)
### Customer Segments: 0, 1, 2, 3, 4, 5

## 🎯 Objectives
- **Identify Customer Segments**: Group customers with similar characteristics and behaviors
- **Behavioral Analysis**: Understand purchasing patterns and customer preferences
- **Business Intelligence**: Provide actionable insights for marketing and sales teams
- **Marketing Strategy**: Enable targeted campaigns and personalized customer experiences
## 🛠️ Technologies Used
- **Python 3.8+**
- **Pandas** - Data manipulation and analysis
- **NumPy** - Numerical computations
- **Matplotlib/Seaborn** - Data visualization
- **Scikit-learn** - Machine learning algorithms
- **Jupyter Notebook** - Interactive development environment
- **Streamlit** - Web app framework
## 📁 Project Structure
```
Customer-Segmentation/
├── notebook/
│ └── customer_segmentation.ipynb # notebook
├── data/
│ └── customer_segmentation.csv   # Dataset
├── model/
│ └── customer_segmentation.pkl   # trained model
├── src/
│ └── app.py                      # web app
├── requirements.txt              # Python dependencies
└── README.md                     # Project documentation
```

### 🔧 Installation & Setup

1. **Clone the repository**
```bash
git clone https://github.com/SamanwoySaha/Customer-Segmentation.git
cd Customer-Segmentation
```
2. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate # On Windows: venv\Scripts\activate
```
3. **Install dependencies**
```bash
pip install -r requirements.txt
```
4. "Run app"
```bash
streamlit run src/app.py
```



