# AI-DRIVEN FRAUDGUARD: ADVANCED FRAUD DETECTION SYSTEM

Welcome to the **Fraud Detection Machine Learning** project! This repository showcases an end-to-end machine learning pipeline to detect fraudulent transactions in financial datasets.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Technologies and Tools Used](#technologies-and-tools-used)
3. [Problem Statement](#problem-statement)
4. [Dataset Description](#dataset-description)
   - [Context](#context)
   - [Features Overview](#features-overview)
5. [Data Ingestion](#data-ingestion)
6. [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
7. [Feature Engineering](#feature-engineering)
8. [Feature Selection](#feature-selection)
9. [Model Training](#model-training)
10. [HyperParameter Tuning](#hyperparameter-tuning)
11. [Model Evaluation](#model-evaluation)
12. [Model Tracking with MLflow](#model-tracking-with-mlflow)
13. [Docker Usage](#docker-usage)
14. [Deployment](#deployment)
15. [Conclusion](#conclusion)

---

## Introduction

Fraud detection is a critical challenge faced by financial institutions, e-commerce platforms, and other industries. The **Fraud Detect AI** project presents an end-to-end machine learning solution to detect fraudulent activities in real-time with high accuracy. This project adheres to industry standards and showcases a robust pipeline, from data ingestion to deployment.

---

## **Technologies and Tools Used**

**Programming Languages**:
- **Python**: Used for machine learning model development and web application creation.

**Libraries & Frameworks**:
- **Scikit-learn**: Utilized for building machine learning models and preprocessing data.
- **XGBoost, LightGBM, CatBoost, AdaBoost**: Employed for training various ensemble models to improve prediction accuracy.
- **Flask**: Used for deploying the trained model as a web application to serve predictions.
- **Pandas, Numpy**: Applied for efficient data manipulation and preprocessing tasks.
- **Matplotlib, Seaborn**: Utilized for data visualization to perform exploratory data analysis and visualize model performance.
- **MLflow**: Integrated for model tracking, versioning, and managing the machine learning lifecycle.

**Cloud & Storage**:
- **Azure Blob Storage**: Used for storing datasets and other large data files in the cloud.

 **Data Ingestion & Storage**:
- **Kaggle**: Leveraged for sourcing datasets, especially for training machine learning models.
- **Azure Blob Storage**: Employed as a secure and scalable cloud-based storage solution for data.

**Version Control**:
- **Git, GitHub**: Utilized for version control, collaboration, and maintaining code repositories.

**Containerization**:
- **Docker**: Used for containerizing the application, ensuring consistency across environments, and simplifying deployment.

**Web Application**:
- **Flask**: Framework used to create a lightweight web application for serving the machine learning model.

**Deployment**:
- **Azure Web Services**: Used for hosting the web application in a scalable cloud environment.

---

## Problem Statement

Fraudulent activities, such as unauthorized transactions and identity theft, cause significant financial losses and damage to brand reputation. Identifying fraud accurately and swiftly is essential to mitigate risks. The challenge lies in distinguishing between genuine and fraudulent activities in a massive dataset with an imbalance between fraudulent and non-fraudulent records.

**Objective**:  
To build a machine learning model capable of detecting fraudulent transactions with high precision and recall while ensuring scalability and real-time inference capabilities.

---

## Dataset Description

### Context

The dataset used in this project is synthetic and generated using the PaySim simulator. It mimics mobile money transactions and includes both normal and fraudulent behaviors to evaluate fraud detection methods.

Dataset 📂 Link: [Kaggle - PaySim Dataset](https://www.kaggle.com/datasets/ealaxi/paysim1/data)

### Features Overview

| **Feature**        | **Description**                                                                                         |
|--------------------|---------------------------------------------------------------------------------------------------------|
| `step`             | Time unit in hours (e.g., 1 step = 1 hour). Total steps = 744 (30 days).                                 |
| `type`             | Type of transaction (e.g., CASH-IN, CASH-OUT, TRANSFER, PAYMENT).                                       |
| `amount`           | Amount of the transaction in local currency.                                                           |
| `nameOrig`         | Customer who initiated the transaction.                                                                |
| `oldbalanceOrg`    | Initial balance of the origin account before the transaction.                                           |
| `newbalanceOrig`   | New balance of the origin account after the transaction.                                                |
| `nameDest`         | Customer who is the recipient of the transaction.                                                      |
| `oldbalanceDest`   | Initial balance of the destination account before the transaction.                                      |
| `newbalanceDest`   | New balance of the destination account after the transaction.                                           |
| `isFraud`          | Indicates if the transaction is fraudulent (1 = Fraud, 0 = Not Fraud).                                  |
| `isFlaggedFraud`   | Indicates if the transaction was flagged as potentially fraudulent by the system.                      |

---

## Data Ingestion

In this step:
- The dataset was first **downloaded** from **Kaggle**.
- It was then **uploaded** to **Azure Blob Storage** for secure storage and accessibility.
- The data was **read** from Blob Storage and **ingested** into the **local project folder** in **CSV format**.

This **CSV file** served as the basis for further **analysis** and **processing**.

---

## Exploratory Data Analysis (EDA)

EDA was conducted to understand the distribution of transactions, the balance between fraud and non-fraud cases, and other insights like transaction types, amounts, and flagged fraud patterns.

---

## Feature Engineering

Feature engineering is a critical step in building a machine learning model, as it involves the creation of new features or the transformation of existing features to enhance model performance. Below are the steps performed in feature engineering for this project:

1. **Handling Missing Values**  
   - **Imputation** was applied to handle any missing values. The missing values were imputed using appropriate strategies such as **mean**, **median**, or **mode** depending on the feature type. However, in this dataset, there were **no missing (NaN) values** found, so this step was not required.

2. **Removing Duplicate Values**  
   - Duplicate rows were identified and **removed** to ensure data integrity. A total of approximately **90,000 duplicate rows** were found and removed from the dataset to ensure the uniqueness of the data and avoid bias in the analysis.

3. **Outlier Detection**  
   - **Outliers** in numerical features were identified and handled using methods like **Z-score** and **IQR (Interquartile Range)**. These methods help to detect values that deviate significantly from the mean, preventing them from skewing the model’s results.

4. **Encoding Categorical Variables**  
   - Categorical features were **encoded** using techniques like **one-hot encoding** to convert categorical variables into numerical values that can be used by machine learning algorithms. Additionally, the **first variable** in each categorical column was dropped to avoid the **dummy variable trap**, which can lead to multicollinearity.

5. **Feature Transformation**  
   - To ensure that numerical features are on the same scale and to improve model performance, **log transformation** was applied to certain numerical features. This transformation helps in handling skewed distributions and makes the features more suitable for machine learning models.

6. **Removing Highly Correlated Features**  
   - Features that were highly **correlated** with one another were removed to prevent multicollinearity. This step ensures that the model remains efficient by eliminating redundant features that do not add significant value to the model’s predictive power.

These transformations help make the data more suitable for training and improve the performance of the fraud detection model.

---

## Feature Selection

Feature selection is a crucial step in improving the model's performance and efficiency by identifying the most important features and eliminating the irrelevant or redundant ones. Below are the steps performed in the feature selection process:

1. **Removal of Irrelevant Features**  
   - **Irrelevant features** that do not contribute meaningfully to the prediction or analysis were **removed**. These features had little to no relationship with the target variable, and retaining them could lead to unnecessary complexity in the model.

2. **Correlation Analysis**  
   - **Correlation analysis** was applied to identify features that were highly correlated with each other. Highly correlated features are often redundant, meaning that they provide similar information. Removing these features prevents **multicollinearity**, which can lead to overfitting and inaccurate model predictions.
   - Features with a correlation coefficient above a specified threshold (typically **0.9**) were removed to avoid redundancy and improve model generalization.

3. **SelectKBest with f_classif**  
   - **SelectKBest** was used with the **f_classif** test to evaluate the significance of each feature in predicting the target variable. The top **K** most significant features were selected based on their **ANOVA F-values**, ensuring that only the most important features were retained.

By performing these steps, we ensured that the dataset was optimized for building the model, with only the most relevant features retained for analysis and prediction.

---

## Model Training

The **model training** process involves defining independent and dependent variables, splitting the dataset, handling class imbalance, scaling features, and training multiple machine learning models. Below are the key steps involved:

1. **Loading the Dataset**
   - The preprocessed dataset is loaded into the system from a specified path and separated into independent variables (`X`) and target variable (`y`).

2. **Splitting the Data**
   - The dataset is split into **training** and **testing** sets, using a **stratified split** to ensure consistent distribution of the target variable across both sets.

3. **Handling Class Imbalance**
   - **SMOTE (Synthetic Minority Oversampling Technique)** is applied to oversample the minority class (fraudulent transactions) in the training data to address the class imbalance.

4. **Feature Scaling**
   - Feature scaling was not performed in this project because we used boosting models such as XGBoost, LightGBM, CatBoost, and AdaBoost. These models are based on decision trees, which are inherently insensitive to the scale of the features. Decision trees work by splitting data based on feature values and do not rely on the distance between data points, making feature scaling unnecessary for tree-based models.

5. **Model Initialization**
   - Multiple machine learning models are initialized, including **XGBoost**, **LightGBM**, **CatBoost**, and **AdaBoost**. These models are selected for their ability to handle imbalanced datasets and their strong performance on structured/tabular data.

6. **Cross-Validation**
   - Stratified K-Fold Cross-Validation is applied during the model training process to ensure the model's performance is robust and not overfitting to a particular subset of the training data. This technique helps in assessing the model’s generalization ability by splitting the training data into several smaller folds and training the model on different folds, then averaging the results.
Training and Saving Models

7. **Training and Saving Models**
   - Each model is trained using the data, and after training, the models are saved for future use.

### Model Performance
- Several models were tested, and **CatBoost** was found to perform the best with an accuracy of **89%**. This model is selected as the final model for deployment.

The trained models are saved in the artifacts/models/ directory for future use.

---

## Hyperparameter Tuning

To optimize model performance, **hyperparameter tuning** was performed on the best-performing models using **RandomizedSearchCV**. These technique allow for searching the best combination of hyperparameters that give the highest model accuracy.

**RandomizedSearchCV**
   - RandomizedSearchCV was used for models like **AdaBoost** and **LightGBM**, as it searches a randomly selected subset of hyperparameters, which can be more efficient than GridSearchCV for larger datasets.
   - RandomizedSearchCV was applied with a set of hyperparameters, such as:
     - **CatBoost Hyperparameters**:
     - iterations: The number of boosting iterations (trees) to train the model. More iterations usually improve performance, but too many can lead to overfitting.
     - depth: The depth of the trees. A larger depth allows the model to capture more complex patterns, but it can also lead to overfitting if set too high.
     - learning_rate: The step size at each iteration. A smaller learning rate improves the model's ability to learn slowly and generalize better, but it requires more iterations.
     - l2_leaf_reg: The regularization term for leaf values to avoid overfitting.
     - subsample: The fraction of samples used to train each tree. Lower values can help reduce overfitting by introducing randomness.
     - cat_features: List of categorical features, as CatBoost can handle categorical data natively.
   
After performing **hyperparameter tuning**, the models with the best parameters were selected for final training. The model performance significantly improved with the chosen hyperparameters, leading to higher accuracy and better classification results.

---

## Model Evaluation

Model evaluation involves assessing the performance of each trained model using key metrics. We use several metrics to evaluate classification models:

- **Accuracy**: The proportion of correct predictions (both true positives and true negatives) out of all predictions.
- **Precision**: The proportion of true positives out of all predicted positives. Precision is important when false positives have a significant impact.
- **Recall**: The proportion of true positives out of all actual positives. Recall is important when false negatives are costly (i.e., missing fraud cases).
- **F1-Score**: The harmonic mean of precision and recall. This metric is particularly useful when the class distribution is imbalanced.
- **AUC-ROC**: The area under the ROC curve, which measures the ability of the model to distinguish between positive and negative classes.

Evaluation Results:
  **CatBoost Model**: 
   - Accuracy: 89%
   - Precision: 0.90
   - Recall: 0.88
   - F1-Score: 0.89
   - ROC-AUC: 0.92


---

## Model Tracking with MLflow:
  - Used MLflow to track the performance and lifecycle of the models.
  - Logged each training run, hyperparameter settings, and evaluation metrics.
  - Enabled easy comparison and reproducibility of models.
  - Ensured transparency in the model’s training process.
  - Allowed monitoring of how hyperparameters impacted the model's performance.
![image](https://github.com/user-attachments/assets/cf36a353-2d70-491f-8449-0d70474995a2)

---

## Docker Usage

In this project, Docker was used to containerize the Flask application for deployment. Below are the steps to use Docker for this project:

Here is a combined list of the process followed along with the commands used:

### Process and Commands:

1. **Create a `Dockerfile`**:  
   Define the steps to build the Docker image, including the base image and necessary dependencies.

2. **Create a `requirements.txt`**:  
   List all the Python dependencies needed for the project (e.g., Flask, scikit-learn).

3. **Build the Docker image**:  
   Run the following command to build the image based on the `Dockerfile`:
   ```bash
   docker build -t fraud-detect-ai .
   ```

4. **Run the Docker container**:  
   After building the image, run the application in a container using this command:
   ```bash
   docker run -p 5000:5000 fraud-detect-ai
   ```

5. **Access the application**:  
   Open your web browser and go to `http://localhost:5000` to interact with the app.

6. **Push the Docker image to Docker Hub**:  
   If you want to share or deploy the image, you can log in to Docker Hub, tag the image, and push it.
   
   - **Login to Docker Hub**:
     ```bash
     docker login
     ```

   - **Tag the image for Docker Hub**:
     ```bash
     docker tag fraud-detect-ai vijaykodam98/fraud-detect-ai
     ```

   - **Push the image to Docker Hub**:
     ```bash
     docker push vijaykodam98/fraud-detect-ai
     ```

     This combines the steps and commands in a simplified workflow for using Docker in project!

---

## Deployment

The trained model is deployed using **Flask**, with a REST API that can accept new transaction data and return predictions (fraudulent or not). The Flask app is containerized using **Docker** to ensure portability and ease of deployment. Finally, the model is deployed on **Azure Web Services**, allowing real-time predictions from users globally.

**Link**: [Fraud Detect AI App](https://frauddetectai-fjf6a9eye4a9bhhf.canadacentral-01.azurewebsites.net/)

![image](https://github.com/user-attachments/assets/e7bae4f7-dbbd-4bb9-a1dd-71c484b738ee)

---

## Conclusion

This project successfully built an end-to-end fraud detection system capable of identifying fraudulent transactions with high accuracy and recall. By leveraging robust machine learning techniques, efficient data preprocessing, and model management tools like MLflow, this system can be integrated into real-time applications for fraud detection in the finance sector.

---
