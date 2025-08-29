---
title: Multiple Disease Prediction
draft: false
tags:
date: 24-Aug-2025
---


[Website](http://ec2-43-204-23-83.ap-south-1.compute.amazonaws.com:8501/) | [Github](https://github.com/SamanwoySaha/Multiple-Disease-Prediction) 

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/) [![Streamlit](https://img.shields.io/badge/Streamlit-1.28%2B-red)](https://streamlit.io/) [![Machine Learning](https://img.shields.io/badge/ML-Scikit%20Learn-orange)](https://scikit-learn.org/)

A comprehensive machine learning-powered web application that predicts multiple diseases including **Diabetes, Heart Disease,** and **Parkinson's Disease**. Built with **Streamlit** for an intuitive user interface and powered by **Support Vector Machine (SVM)** and **Logistic Regression** algorithms.

![](https://i.postimg.cc/7Y4XSMDF/multiple-disease-prediction.png)

## 🌟 Features

- **Multi-Disease Prediction**: Predict Diabetes, Heart Disease, and Parkinson's Disease
- **High Accuracy Models**: Trained on medical datasets with optimized algorithms
- **User-Friendly Interface**: Clean, intuitive Streamlit web interface
- **Real-time Results**: Instant predictions with confidence scores
- **Responsive Design**: Works seamlessly across devices
- **Privacy-First**: No data storage, all processing done locally
- 🔄 **Automated CI/CD Pipeline**: Complete GitHub Actions workflow with testing, Docker builds, and AWS EC2 deployment

## 📊 Model Performance

### 1. 💉 Diabetes Prediction

- **Algorithm**: Support Vector Machine (Linear Kernel)
- **Features**: 8 (Glucose, Blood Pressure, BMI, Age, etc.)
- **Training Accuracy**: 78%
- **Test Accuracy**: 77%
- **Dataset Size**: 768 samples
### 2. ❤️ Heart Disease Prediction

- **Algorithm**: Logistic Regression
- **Features**: 13 (Chest Pain, Cholesterol, Heart Rate, etc.)
- **Training Accuracy**: 84%
- **Test Accuracy**: 78%
- **Dataset Size**: 303 samples
### 3. 🧠 Parkinson's Disease Prediction

- **Algorithm**: Support Vector Machine (Linear Kernel)
- **Features**: 22 (Voice measurements and tremor analysis etc.)
- **Training Accuracy**: 88%
- **Test Accuracy**: 87%
- **Dataset Size**: 195 samples
## 📊 Dataset Information

### Data Sources
- **Diabetes**: Pima Indians Diabetes Database
- **Heart Disease**: UCI Heart Disease Dataset
- **Parkinson's**: Oxford Parkinson's Disease Detection Dataset
### Data Preprocessing

- Missing value handling
- Feature scaling and normalization
- Train-test split (80-20)

## 🛠️ Technology Stack

| Technology                                                                                                     | Purpose             | Version  |
| -------------------------------------------------------------------------------------------------------------- | ------------------- | -------- |
| ![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)                   | Core Programming    | 3.8+     |
| ![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat&logo=streamlit&logoColor=white)          | Web Interface       | 1.28+    |
| ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)                   | Data Processing     | 2.0+     |
| ![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)                      | Numerical Computing | 1.24+    |
| ![Scikit-Learn](https://img.shields.io/badge/Scikit_Learn-F7931E?style=flat&logo=scikit-learn&logoColor=white) | Machine Learning    | 1.3+     |
| ![Pickle](https://img.shields.io/badge/Pickle-3776AB?style=flat&logo=python&logoColor=white)                   | Model Serialization | Built-in |

### DevOps & Deployment Stack

| Technology                                                                                                           | Purpose              | Version |
| -------------------------------------------------------------------------------------------------------------------- | -------------------- | ------- |
| ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat&logo=github-actions&logoColor=white) | CI/CD Pipeline       | Latest  |
| ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)                         | Containerization     | 24.0+   |
| ![DockerHub](https://img.shields.io/badge/DockerHub-2496ED?style=flat&logo=docker&logoColor=white)                   | Container Registry   | Latest  |
| ![AWS EC2](https://img.shields.io/badge/AWS_EC2-FF9900?style=flat&logo=amazon-aws&logoColor=white)                   | Cloud Infrastructure | Latest  |

### 🔄 CI/CD Pipeline Overview

The pipeline consists of three main stages:
1. 🧪 Testing Stage: Validates code quality and executes Jupyter notebooks
2. 🏗️ Build & Push Stage: Creates Docker images and pushes to DockerHub
3. 📦 Docker Containerization: Automatically builds optimized Docker images
4. 🐳 DockerHub Integration: Seamlessly pushes images to DockerHub registry
5. Deployment Stage: Automatically deploys to AWS EC2 with zero downtime
6. ☁️ Cloud Deployment: Deploys directly to AWS EC2 instances
7. 🔄 Zero-Downtime Deployment: Rolling updates without service interruption
8. 🧹 Resource Optimization: Automatic cleanup of unused Docker resources
9. 📊 Build Caching: Optimized build times using GitHub Actions cache
## Quick Start
### Prerequisites
```bash
Python 3.8+
pip package manager
```
### Local Setup

#### Installation
1. **Clone the repository**
```bash
git clone https://github.com/SamanwoySaha/Multiple-Disease-Prediction.git
cd Multiple-Disease-Prediction
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

4. **Run the application**
```bash
streamlit run app.py
```

5. **Open your browser**

```
Navigate to: http://localhost:8501
```

#### Run the app from Docker Image

1. Pull the image from Docker Hub
```bash
docker pull samanwoysaha/multiple-disease-prediction:latest
```

2. Run the image
```bash
docker run -p 8501:8501 samanwoysaha/multiple-disease-prediction:latest
```

3. **Open your browser**

```
Navigate to: http://localhost:8501
```

## 📁 Project Structure

```
Multiple-Disease-Prediction/
├── src/
| ├── 📄 app.py # Main Streamlit application
├── 📊 models/
│ ├── diabetes_model.sav # Trained diabetes prediction model
│ ├── heart_disease_model.sav # Trained heart disease model
│ └── parkinsons_model.sav # Trained Parkinson's model
├── 📓 notebooks/
│ ├── diabetes_prediction.ipynb # Diabetes model training notebook
│ ├── heart_disease_prediction.ipynb # Heart disease training notebook
│ └── parkinsons_prediction.ipynb # Parkinson's training notebook
├── 📂 data/
│ ├── diabetes.csv # Diabetes dataset
│ ├── heart_disease.csv # Heart disease dataset
│ └── parkinsons.csv # Parkinson's dataset
├── 🔧 requirements.txt # Python dependencies
├── 📚 README.md # Project documentation
```

## 📈 Future Enhancements

- [ ] **Additional Diseases**: Liver disease, kidney disease, cancer prediction
- [ ] **Deep Learning Models**: Implement neural networks for better accuracy
- [ ] **Mobile App**: React Native or Flutter mobile application
- [ ] **Advanced Visualizations**: Interactive charts and graphs
- [ ] **User Authentication**: Login system with prediction history
- [ ] **Telemedicine Integration**: Connect with healthcare providers
- [ ] **Multi-language Support**: Support for regional languages





  

