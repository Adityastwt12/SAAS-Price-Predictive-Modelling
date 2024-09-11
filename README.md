# Predictive Pricing Model for Enterprise SaaS Products

## **Overview**

This project aims to develop a predictive pricing model for enterprise SaaS (Software as a Service) products. The goal is to assist CIOs, CTOs, and other decision-makers in determining a fair market price for SaaS products, balancing the interests of both buyers and sellers. The model leverages various features such as location, keywords, tech stack, listing type, customer size, and financial metrics to predict the asking price of SaaS businesses.

## Table of Contents

- [Objective](#objective)
- [Installation](#installation)
- [Data Description](#data-description)
- [Synthetic Data Generation](#synthetic-data-generation)
- [Data Preprocessing](#data-preprocessing)
- [Feature Correlation Analysis](#feature-correlation-analysis)
- [Model Development](#model-development)
- [Inference](#inference)
- [Price Predictor Application](#price-predictor-application)
- [Conclusion](#conclusion)
- [License](#license)


## Objective

Accurately pricing SaaS products is crucial for ensuring competitiveness and profitability in the market. The challenge lies in considering multiple factors like geographic location, technological stack, business age, and customer base, which can significantly influence the price. This project addresses this challenge by building a robust predictive model to estimate the asking price based on historical data and business characteristics.

## Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/a-r-p-i-t/SAAS-Price-Predictive-Modelling.git


2. **Install the required modules:**

    ```bash
    cd SAAS-Price-Predictive-Modelling
    pip install pandas -r requirements.txt


## **Data Description**

The dataset used in this project includes various features relevant to SaaS businesses:

- **Numeric Features**:
  - `revenueMultiple`: The revenue multiple of the business.
  - `totalRevenueAnnual`: The total annual revenue.
  - `team`: Number of team members.
  - `revenue`: Current revenue.
  - `annualProfit`: Annual profit.
  - `growthAnnual`: Annual growth rate.
  - `weeklyViews`: Weekly views or impressions.
  - `businessAge`: Age of the business in years.

- **Categorical Features**:
  - `location`: The geographic location of the business (e.g., United States, Germany).
  - `keywords`: Descriptive keywords about the business (e.g., HealthCare, Finance).
  - `techStack`: The technological stack used by the business (e.g., FullStack, Automation).
  - `listingType`: Type of listing (e.g., premium, platinum).
  - `customers`: Customer base size category (e.g., 100-1000, 1000-10000).
 

## **Assumptions**

In this project, we make several assumptions about the input data to ensure the model's predictions are accurate and meaningful. These assumptions are based on the observed distribution and characteristics of the dataset.

1. **Numeric Features**: The input values should be within the following ranges to be considered valid:

   - **`revenueMultiple`**: The revenue multiple of the business should be between **0** and **11.33955**.
   - **`totalRevenueAnnual`**: The total annual revenue should be between **128** and **2,439,655**.
   - **`team`**: The number of team members should be between **0** and **20**.
   - **`revenue`**: The current revenue should be between **57** and **2,148,792**.
   - **`annualProfit`**: The annual profit should be between **-251,864** (indicating a loss) and **557,274**.
   - **`growthAnnual`**: The annual growth rate should be between **0%** and **384.85%**.
   - **`weeklyViews`**: The number of weekly views should be between **0** and **21**.
   - **`businessAge`**: The age of the business in years should be between **0** and **14.66**.

2. **Categorical Features**: The input values should be one of the following valid options:

   - **`location`**: 
     - United States, United Kingdom, Canada, France, Switzerland, Estonia, Ukraine, Spain, Australia, Germany, Austria, Latvia, Belgium, Turkey, Mexico, Singapore, India, Argentina.
   
   - **`keywords`**:
     - Automation, Web Tools, Analytics, Technology, Management, HealthCare, Mobile App, Sales, Finance, SEO, FundRaiser, Workforce, Servers, Entertainment, E-Commerce, Loyalty, Games, Enterprise, Marketing, Security, EdTech, Telecommunication, HRTech.
   
   - **`techStack`**:
     - FullStack and Cloud, BackEnd and Cloud, Cloud, BackEnd, FullStack, FrontEnd, FullStack and DBMS, FrontEnd and Cloud, Backend, Not Listed, Backend and DBMS, Cloud and DBMS, CyberSecurity, DBMS.

   - **`listingType`**:
     - platinum, premium.

   - **`customers`**:
     - 10-100, 100-1000, 1000-10000, 10000-100000, more than 100000.

3. **Data Verification**: It is assumed that all data inputs provided by the company at the time of registering the product are verified and true. This means the model operates under the assumption that there are no errors or falsifications in the input data provided by businesses.
   
4. **Customer Negotiation**: For customers, it is assumed that they generally settle within **15%** of the asking price of the product. The asking price may be updated based on customer satisfaction and product feasibility reviews. This ensures that the price is competitive and aligns with customer expectations and market standards.
   
5. **Company Pricing Strategy**: For companies, the asking price shown is typically set at **50% more than the original cost**. This pricing strategy is designed to provide a **40% margin** for the seller to negotiate with potential buyers, allowing flexibility in pricing negotiations to meet both buyer and seller expectations.



## **Synthetic Data Generation**

The original dataset from Kaggle contained only 127 data points, which was not sufficient for building a robust predictive model. To help the model converge better and learn from a richer dataset, we scaled up the data using **synthetic data generation** with the **CTGAN (Conditional Generative Adversarial Network)** model. 

- **CTGAN** was used to generate 10,000 synthetic data samples that match the distribution and characteristics of the original dataset.
- **Table Evaluator** was employed to visually assess and validate how well the synthetic data aligns with the original data in terms of distributions, correlations, and overall patterns.

<img src="https://github.com/user-attachments/assets/1d507365-81c9-4b8d-b418-4e83751905b1" alt="Screenshot 2024-09-04 031352" width="700">
<br><br><br><br>
<img src="https://github.com/user-attachments/assets/ebf8fa3e-86ea-45d9-a045-ab79fd7de1ea" alt="Screenshot 2024-09-04 031657" width="1200">
<br><br><br><br>
<img src="https://github.com/user-attachments/assets/d2690eeb-acc7-4d19-b35f-cd8da91ebf64" alt="Screenshot 2024-09-04 031619" width="400">
<br><br><br><br>
<img src="https://github.com/user-attachments/assets/1f6e7a34-532d-4039-b38b-7560e12d8d93" alt="Screenshot 2024-09-04 031516" width="350" style="vertical-align: top;"/>
<br><br><br><br>
<img src="https://github.com/user-attachments/assets/b482cc5a-66d7-49e7-91a1-a547308714d5" alt="Screenshot 2024-09-04 031527" width="320" style="vertical-align: top;"/>
<br><br><br><br>
<img src="https://github.com/user-attachments/assets/86304ec8-4cc6-4f30-a794-79d913cc4973" alt="Screenshot 2024-09-04 031453" width="320" style="vertical-align: top;"/>
<br><br><br><br>
<img src="https://github.com/user-attachments/assets/e8ed4897-0b04-4621-8fe4-53b3160d3782" alt="Screenshot 2024-09-04 031535" width="320" style="vertical-align: top;"/>
<br><br><br><br>
<img src="https://github.com/user-attachments/assets/93871ec0-2b0a-4ccc-8385-f3a166f36c3b" alt="Screenshot 2024-09-04 031420" width="310" style="vertical-align: top;"/>










## **Data Preprocessing**

Several preprocessing steps were performed to clean and prepare the data:

1. **Date Preprocessing & Feature Engineering**:
   - Converted `date` and `dateFounded` to datetime format.
   - Calculated `businessAge` as the difference between `date` and `dateFounded`.

2. **Handling Missing Values**:
   - Filled missing values in the `location` column with "United States".
   - Dropped `totalGrowthAnnual' column due to high amount of missing values.

3. **Encoding**:
   - One-Hot Encoded categorical features to convert them into numeric entities, as required to input the model..

4. **Outlier Removal**:
   - Used the IQR (Interquartile Range) method to remove outliers from numeric features.

5. **Data Augmentation**:
   - Employed CTGAN (Conditional Generative Adversarial Networks) to generate synthetic samples for data balancing and enhancing model training.
   - Data is scaled from 127 data points to 10000 data points to help model generalize and converge better.
  
## **Feature Correlation Analysis**

To understand the relationships between different features and identify potential multicollinearity issues, a correlation matrix was computed for the numeric features in the dataset. A heatmap was then plotted to visualize these correlations.

- **Correlation Matrix**: Shows the Pearson correlation coefficients between pairs of numeric features, indicating the strength and direction of their linear relationships.
- **Heatmap**: Provides a visual representation of the correlation matrix, using color gradients to illustrate the magnitude of correlations.

The correlation matrix and heatmap help in identifying strongly correlated features that could be redundant or have multicollinearity, guiding feature selection and engineering decisions.

<img src="https://github.com/user-attachments/assets/5b90d935-0051-48bd-acec-58b6175bb572" alt="Screenshot 2024-09-04 050101" width="600">


## **Model Development**

### **Algorithm Choice**

The model utilizes the **XGBoost Regressor**, a robust and efficient implementation of gradient-boosted decision trees designed for supervised learning. XGBoost is chosen for its **High Performance**, abilitity to capture **Non-Linearity** in the dataset, and **Scalability**.

### **Fine-Tuned Hyperparameters**

- `n_estimators`: 500
- `learning_rate`: 0.05
- `max_depth`: 6
- `subsample`: 0.8
- `colsample_bytree`: 0.8
- `random_state`: 42

### **Cross-Validation and Model Evaluation**

To evaluate the model, 5-Fold Cross-Validation was performed using the following metrics:

- **Mean Squared Error (MSE)**
- **R-squared (R²)**
- **Root Mean Squared Error (RMSE)**
- **Mean Absolute Percentage Error (MAPE)**

Cross-validation results:
- **Average Cross-Validation MSE**: 518728851546.0179
- **Average Cross-Validation RMSE**: 720228.3329
- **Average Cross-Validation R²**: 0.6238
- **Average Cross-Validation MAPE**: 1.1109%

### **Final Model Training**

After cross-validation, the model was trained on the entire training dataset to leverage all available data and improve predictive accuracy.

### **Model Evaluation on Test Data**

The model was evaluated on the test dataset with the following performance metrics:

- **Test Data MSE**: 494330258465.4773
- **Test Data R²**: 0.6282
- **Test Data RMSE**: 703086.2383
- **Test Data MAPE**: 2.1806%

<img src="https://github.com/user-attachments/assets/a3638b6b-5f3a-479d-8772-5bd89f05ebf0" alt="Screenshot 2024-09-04 082037" width="700">




### **Model Saving**

The trained XGBoost model was saved using `joblib` for future use and deployment.

1. ```bash
   joblib.dump(xgb_model, 'xgb_model.pkl')

   
## **Inference**


The inference script is designed to predict the asking price of a SaaS business based on user-provided input data. The script includes two main functions:

1. **`preprocess_input(user_input)`**: Prepares the user input data by transforming it into the same format used during the model's training process.
2. **`predict_asking_price(user_input)`**: Uses the trained XGBoost model to predict the asking price based on the preprocessed input data.

### **Function Descriptions**

1. **`preprocess_input(user_input)`**:

   This function converts raw user input into a structured format that matches the training data format. 

   - **Input**: A dictionary (`user_input`) containing user-provided information about the SaaS business, such as `revenueMultiple`, `location`, `techStack`, and other relevant features.
   - **Output**: A pandas DataFrame (`input_data`) with the same columns as the training dataset, where categorical variables are one-hot encoded, and numeric variables are directly filled.

   **Steps**:
   - **Initialize an Empty DataFrame**: Creates a DataFrame with columns matching those used in training (`original_columns`).
   - **Fill Numeric Features**: Directly inserts numeric values from `user_input` (like `revenueMultiple`, `totalRevenueAnnual`, etc.) into the corresponding columns.
   - **One-Hot Encode Categorical Features**: 
     - Initializes all one-hot encoded categorical columns to `0`.
     - Sets the appropriate column to `1` based on the user input, simulating the one-hot encoding process used during model training.
   - **Ensure Consistency**: Converts all data to numeric types to ensure compatibility with the model’s input format.

2. **`predict_asking_price(user_input)`**:

   This function predicts the asking price using the trained XGBoost model.

   - **Input**: A dictionary (`user_input`) containing input data for a single SaaS business.
   - **Output**: A float representing the predicted asking price.

   **Steps**:
   - **Preprocess Input Data**: Calls `preprocess_input(user_input)` to transform the raw input into a model-compatible format.
   - **Predict Using XGBoost Model**: Uses the loaded XGBoost model (`xgb_model`) to make a prediction based on the preprocessed input data.
   - **Return Prediction**: Outputs the predicted asking price.

### **Example Usage**

To use the inference script, provide a dictionary with the required input data. The script preprocesses this data to align with the model's training format, then feeds it into the trained XGBoost model to generate a prediction.

```python
user_input = {
    'revenueMultiple': 11.085633,
    'totalRevenueAnnual': 596005,
    'team': 8,
    'listingType': 'platinum',
    'revenue': 411238.250173,
    'customers': '100-1000',
    'annualProfit': 7459,
    'growthAnnual': 125.167142,
    'weeklyViews': 6,
    'businessAge': 5.128171,
    'location': 'United States',
    'keywords': 'HealthCare',
    'techStack': 'FullStack and Cloud',
}

predicted_price = predict_asking_price(user_input)
print(f"Predicted Asking Price: ${predicted_price:.2f}")
```

## **Price Predictor Application**

### **Overview**

The **Price Predictor Application** is a desktop application that provides a convenient way for both customers and companies to interact with product pricing and registration. The application features a graphical user interface (GUI) built using **Tkinter** and is designed to offer a seamless experience for users.

### **Features**

1. **User Registration**
   - **Customer Registration**: Allows customers to sign up and view a list of products registered by various companies. Customers can see the asking price for each product and any discounts offered.
   - **Company Registration**: Enables companies to register their products by filling out the necessary details. Upon submission, the application predicts a suitable asking price for the product and provides an estimated cost of production.

2. **Product Listing**
   - **For Customers**: View a comprehensive list of products available on the platform, complete with prices and discounts.
   - **For Companies**: Register new products, view predicted prices, and access production cost estimates. Once a product is registered, it becomes visible to all customers on the platform.

### **Installation**

The application is packaged as a standalone executable. To install and run the application, follow these steps:
1. **Clone the repository:**

   ```bash
   git clone https://github.com/a-r-p-i-t/SAAS-Price-Predictive-Modelling.git

2. **Run the Python Script**:

   cd SAAS-Price-Predictive-Modelling.git
   <br>
   Run the **[app.py](./app.py)** script to start the application. No additional installation steps are required.

### **Usage**

1. **Launch the Application**: Run the **[app.py](./app.py)** script to open the application.
2. **Register/Login**: Choose to register or log in as either a customer or a company.
   - If you are a **customer**, you will be directed to the product listing page.
   - If you are a **company**, you will be prompted to enter your product details, after which the application will predict a suitable price and display the production cost.
3. **View or Register Products**: Depending on your role, you can either view the products available on the platform or register a new product.

### **Technical Details**

- **GUI Framework**: Tkinter
- **Machine Learning Model**: Used for predicting product prices based on the information provided by companies.

### **Contact**

For any issues or inquiries, please contact **[Arpit Mohanty]** at **[arpitmohanty222@gmail.com]**.

## **Conclusion**

The Predictive Pricing Model for Enterprise SaaS Products is a powerful tool designed to assist decision-makers in determining fair market prices for SaaS businesses. By leveraging advanced machine learning techniques and a robust set of features, the model provides accurate and reliable pricing predictions that balance the interests of both buyers and sellers. The integration of synthetic data generation has enhanced the model's performance by increasing the dataset size, enabling better generalization and convergence. Additionally, the Price Predictor Application offers a user-friendly interface, allowing both customers and companies to easily interact with the platform and access valuable pricing insights.

This project demonstrates the potential of machine learning in solving complex business problems and provides a framework that can be expanded and adapted to other domains. Future work may include the integration of more sophisticated features, such as real-time market analysis and external economic indicators, to further improve pricing accuracy and adapt to market changes.


## License

MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
