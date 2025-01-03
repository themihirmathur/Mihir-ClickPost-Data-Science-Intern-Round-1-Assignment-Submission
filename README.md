# Estimated Delivery Date (EDD) Prediction | ClickPost Data Science Internship Assignment

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

## Problem Statement
`Logistics` is a critical sector with millions of daily shipments. Predicting the exact Estimated Delivery Date (EDD) for each order is essential for enhancing customer experience and optimizing operational efficiency. The objective of this project is to predict the `predicted_exact_sla`, which is the number of days between the shipment and delivery of an order, using historical shipment data.

![Screenshot 2024-12-22 at 9 13 28 PM](https://github.com/user-attachments/assets/12efa205-8001-48a8-85d1-025a9f511fbd)

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

## **Dataset**
The dataset provided consisted of three files:
1. `train.csv`: Historical shipment data from June 2022 to August 2022 for model training.
2. `test.csv`: Shipment data for the subsequent three weeks for which predictions are to be made.
3. `pincodes.csv`: A list of pincodes with corresponding geographic details.

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

### **Fields in the Dataset**
- **order_shipped_date**: Date when the shipment was shipped.
- **order_delivered_date**: Date when the shipment was delivered (in `train.csv` only).
- **pickup_pin_code** and **drop_pin_code**: Geographic locations of the origin and destination.
- **quantity**: Number of items in the order.
- **courier_partner_id**: Identifier for the courier partner.
- **account_type_id** and **account_mode**: Account-related details.
- **order_delivery_sla**: Promised SLA for delivery (in `train.csv` only).

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

## **Steps to Solve the Problem**

### **1. Data Preprocessing**
1. **Date Parsing**: Converted `order_shipped_date` and `order_delivered_date` to datetime objects.
2. **Feature Engineering**:
  - Computed `actual_sla` (number of days between shipment and delivery) for training.
  - Extracted additional features such as the weekday of shipping.
3. **Encoding Categorical Variables**:
  - Used label encoding for features like `courier_partner_id`, `account_type_id`, and `account_mode`.
4. **Geographic Features**:
  - Merged `pincodes.csv` to calculate geographic distances between `pickup_pin_code` and `drop_pin_code`.
5. **Outlier Detection and Removal**:
   - Removed outliers in `actual_sla` using the IQR method.
6. **Handling Missing Values**:
   - Imputed missing numerical values with their median and categorical values with their mode.
7. **Duplicate Removal**:
   - Dropped duplicate rows from the dataset.

![Screenshot 2024-12-22 at 8 59 39 PM](https://github.com/user-attachments/assets/ffdad7ee-3bca-42d0-b1b9-1760f24316bd)

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

### **2. Model Selection**
I selected **RandomForestRegressor** for this task due to:
- Its ability to handle both numerical and categorical data efficiently.
- Robustness to outliers, resistance to overfitting, and low requirement for feature scaling.
- Built-in feature importance evaluation to identify key drivers for predictions.

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

### **3. Model Training and Validation**
1. **Training Dataset**:
   - Three models were trained, evaluated, and then used by a meta-model (with Linear Regression): RandomForestRegressor, XGBoost, and LightGBM.
2. **Evaluation Metrics**:
   - **Root Mean Squared Error (RMSE):** `0.4577`
   - **Mean Absolute Error (MAE):** `0.2763`
   - **R² Score:** `0.7592`
3. **Alternative Models**:
   - Trained and evaluated additional models, including XGBoost and LightGBM. However, RandomForestRegressor outperformed them in terms of RMSE.

![Screenshot 2024-12-22 at 8 59 30 PM](https://github.com/user-attachments/assets/6c289cbc-4d2d-4448-a047-d573d833b28f)

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

### **4. Predictions**
- Used the trained model to predict `predicted_exact_sla` for the `test.csv` data.
- The predictions were saved in a file named `submission.csv`, as required.

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

### **5. Data Visualization**
- **Feature Importance**: 
  - Displayed the relative importance of each feature using the Random Forest model.
  - Key Features:
    - `courier_partner_id`: 37.35%
    - `drop_pin_code`: 36.63%
    - `order_shipped_date`: 14.69%
    - `pickup_pin_code`: 8.78%
- **Distribution of Predictions**:
  - Visualized the distribution of predicted SLAs to identify trends and potential outliers.

![Screenshot 2024-12-22 at 8 59 15 PM](https://github.com/user-attachments/assets/37f206b6-e65d-44b9-a078-222e757acec3)

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

### **6. Engineering Document**

To integrate the model into the ClickPost system:
1. **Data Pipeline**:
   - Develop a pipeline to preprocess shipment details in real-time.
2. **Model Deployment**:
   - Deploy the trained model as an API using Flask or FastAPI.
   - Enable both single and batch prediction endpoints.
3. **Database Integration**:
   - Store predicted SLAs in the database for operational monitoring.
4. **Dashboard Integration**:
   - Visualize predicted EDD values in ClickPost's logistics dashboards.
5. **Monitoring and Retraining**:
   - Monitor model performance and retrain periodically to adapt to changing logistics trends.

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

## **Deliverables**
1. **`submission.csv`**: File containing the predicted `predicted_exact_sla` for the test data.
2. **Model Description**: Explained the RandomForestRegressor model and its variable importance.
3. **Data Visualization**: Feature importance and SLA prediction distribution graphs.
4. **Engineering Document**: Steps for integrating the EDD model into ClickPost's system.

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

## Future Work

1. **Data Preprocessing**:  
   - Handle missing values more effectively to ensure data quality.

2. **Feature Engineering**:  
   - Add features such as geographic distance using latitude and longitude from `pincodes.csv`.  
   - Incorporate indicators for weekends and weekdays to capture temporal effects.

3. **Integration into ClickPost**:
  
   a. **Deployment**:  
      - Convert the model to a REST API using Flask or FastAPI.  
      - Handle real-time predictions via JSON requests.  

   b. **Batch Processing**:  
      - Enable bulk predictions for large datasets via CSV uploads.  

   c. **Monitoring**:  
      - Log predictions and compare them with actual SLAs.  
      - Periodically refine the model based on performance metrics.  

---

## **Contact**
If you have any questions or feedback, feel free to reach out:  
**Name**: Mihir Mathur  
**Email**: [themihirmathur@gmail.com](mailto:themihirmathur@gmail.com)  
**Phone**: +91-7525099328  

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>
