
# Medical Insurance Cost Prediction  

This project trains and deploys a locally running machine learning model for predicting an individual’s medical insurance charges based on demographic and health data.  

---

## 📊 Dataset  
The model was trained on the [Medical Insurance Cost Dataset](https://www.kaggle.com/datasets/mosapabdelghany/medical-insurance-cost-dataset) from Kaggle.  

**Features include:**  
- `age` (numeric)  
- `sex` (binary: 0 = female, 1 = male)  
- `bmi` (numeric)  
- `children` (numeric)  
- `smoker` (binary: 0 = non-smoker, 1 = smoker)  
- `region` (one-hot encoded: northwest, southeast, southwest, northeast [baseline])  

---

## 🤖 Model  
A **linear regression model** was chosen for its interpretability and suitability for continuous outcomes.  
We compared:  
- Ordinary Linear Regression  
- Regularized models: **Ridge**, and **ElasticNet**  

**Evaluation Metrics:**  
- Root Mean Squared Error (RMSE)  
- R² Score (on training and test sets)  

📌 Regularization did not significantly improve performance, so **ordinary linear regression** was selected as the final model.  

The code used for training the linear regression model is available in a **Google Colab notebook**:  
[Open Colab Notebook](https://colab.research.google.com/drive/1z4wuowh5jqf758zdt85syZEAoCn0hJdm#scrollTo=bn2DRnsoPTw4)

This notebook includes:  
- Preliminary analysis of the dataset
- Data preprocessing steps (handling categorical variables, scaling numeric features)  
- Model training (ordinary linear regression and comparisons with regularized models)  
- Evaluation metrics (RMSE, R²)  
- Visualization of results 
---

## Deployment  
The trained model is deployed using a simple **Flask** web server.  

- Accepts **JSON input** with feature values  
- Returns predicted insurance cost as **JSON output**  

---

## ⚙️ Installation  

Clone the repository and install dependencies:  

```bash
git clone https://github.com/Agedis/and-global-assignment.git
cd and-global-assignment

python app.py (the server will start locally by default assuming all the necessary packages are installed)
```

## Example JSON request
{
  "age": 19,
  "sex": 1,
  "bmi": 140,
  "children": 0,
  "smoker": 0,
  "region_northwest": 0,
  "region_southeast": 0,
  "region_southwest": 1
}

### ⚠️ Input Preconditions  

When sending JSON input to the API, please ensure the following:  

- **Age**: Must be a positive integer (e.g., `19`).  
- **Sex**: Encoded as `0` (female) or `1` (male).  
- **BMI**: Must be a positive float or integer (e.g., `27.9`).  
- **Children**: Non-negative integer (e.g., `0`, `1`, `2`, …).  
- **Smoker**: Encoded as `0` (non-smoker) or `1` (smoker).  
- **Region**: Represented with one-hot encoding:  
  - `region_northwest`, `region_southeast`, `region_southwest`  
  - Each takes a value of `0` or `1`.  
  - **Exactly one** region should be `1`, and the others must be `0`.  
  - Example: `"region_southwest": 1, "region_southeast": 0, "region_northwest": 0`  

If these conditions are not met, the model’s predictions may be unreliable or the server may throw an error.  

## Example output
{
  "predicted_insurance_cost": 45231.78
}

## 📦 Packages Used  

The project makes use of the following Python packages:  

- [scikit-learn](https://scikit-learn.org/stable/) – Machine learning models (Linear Regression, Ridge, ElasticNet)  
- [numpy](https://numpy.org/) – Numerical computations  
- [pandas](https://pandas.pydata.org/) – Data manipulation and preprocessing  
- [matplotlib](https://matplotlib.org/) – Data visualization  
- [seaborn](https://seaborn.pydata.org/) – Statistical data visualization  
- [flask](https://flask.palletsprojects.com/) – Web framework for deployment  
- [json](https://docs.python.org/3/library/json.html) – JSON parsing and formatting  
- [sys](https://docs.python.org/3/library/sys.html) – System-specific parameters and functions 
