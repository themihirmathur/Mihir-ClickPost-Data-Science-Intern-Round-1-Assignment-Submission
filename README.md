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
- **Date Parsing**: Converted `order_shipped_date` and `order_delivered_date` to datetime objects.
- **Feature Engineering**:
  - Computed `actual_sla` (number of days between shipment and delivery) for training.
  - Extracted additional features such as the weekday of shipping.
- **Encoding Categorical Variables**:
  - Used label encoding for features like `courier_partner_id`, `account_type_id`, and `account_mode`.
- **Geographic Features**:
  - Merged `pincodes.csv` to calculate geographic distances between `pickup_pin_code` and `drop_pin_code`.

![Screenshot 2024-12-22 at 8 59 39 PM](https://github.com/user-attachments/assets/ffdad7ee-3bca-42d0-b1b9-1760f24316bd)

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

### **2. Model Selection**
I selected **RandomForestRegressor** for this task due to:
- Its ability to handle both numerical and categorical data.
- Resistance to overfitting with hyperparameter tuning.
- Built-in feature importance evaluation.

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>

### **3. Model Training and Validation**
- **Training Dataset**: Split the training data into an 80:20 ratio for training and validation.
- **Evaluation Metrics**:
  - Root Mean Squared Error (RMSE): 0.7601
  - Mean Absolute Error (MAE): 0.3645
  - R² Score: 0.8074
- Hyperparameter tuning using GridSearchCV further improved model performance.

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

---

## **Contact**
If you have any questions or feedback, feel free to reach out:  
**Name**: Mihir Mathur  
**Email**: [themihirmathur@gmail.com](mailto:themihirmathur@gmail.com)  
**Phone**: +91-7525099328  

<p align="left">
  <img src="https://www.animatedimages.org/data/media/562/animated-line-image-0184.gif" width="1920" 
</p>
