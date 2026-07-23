Pregnancy Risk Prediction System

A Python machine learning project that estimates pregnancy risk from personal, medical, and pregnancy-history information.

The project includes:

A Streamlit web application

A command-line prediction program

A model-training and model-selection script

A saved Scikit-learn prediction pipeline

Automatic BMI calculation

Pregnancy-risk percentage and risk-level display

Medical disclaimer: This project is intended only for education, academic demonstration, and portfolio use. It is not a medical diagnosis system and must not replace professional medical advice, examination, or treatment.

Project Features

Accepts personal and medical information from the user

Calculates BMI from height and weight

Accepts blood sugar in mmol/L

Converts blood sugar to mg/dL for display in the web application

Predicts a pregnancy-risk percentage

Categorizes the predicted risk as:

Low: below 33%

Medium: 33% to below 66%

High: 66% or above

Supports both web-based and terminal-based prediction

Handles missing feature values using mean imputation

Standardizes input features before model prediction

Compares Random Forest, Decision Tree, and Logistic Regression models

Saves the selected model as best_model_dataset_1.pkl

Project Structure

Pregnancy_Risk_Prediction_System/
│
├── app.py
├── user_input.py
├── model_training_dataset_1.py
├── dataset_1.csv
├── best_model_dataset_1.pkl
├── requirements.txt
└── README.md

File Description

File

Purpose

app.py

Runs the Streamlit web application

user_input.py

Runs pregnancy-risk prediction in the terminal

model_training_dataset_1.py

Cleans the dataset, compares models, evaluates the best model, and saves it

dataset_1.csv

Contains the pregnancy-risk training data

best_model_dataset_1.pkl

Contains the saved trained Scikit-learn pipeline

requirements.txt

Lists the required Python packages

README.md

Explains the project and its usage

Dataset

The project uses dataset_1.csv, based on the Maternal Health and High-Risk Pregnancy Dataset.

Dataset source:

Maternal Health and High-Risk Pregnancy Dataset on Kaggle

The included dataset contains:

1,205 rows

11 input features

1 target column named Risk Level

The target values are:

Low

High

Rows with a missing Risk Level are removed before training.

Input Features

Feature

Description

Age

Age of the pregnant person

Systolic BP

Systolic blood pressure

Diastolic

Diastolic blood pressure

BS

Blood sugar level in mmol/L

Body Temp

Body temperature in Fahrenheit

BMI

Body mass index

Previous Complications

Previous pregnancy complications: 0 or 1

Preexisting Diabetes

Pre-existing diabetes: 0 or 1

Gestational Diabetes

Gestational diabetes: 0 or 1

Mental Health

Stress, anxiety, or depression history: 0 or 1

Heart Rate

Heart rate in beats per minute

Machine Learning Workflow

1. Data Loading

The training script loads the dataset using Pandas:

df = pd.read_csv("dataset_1.csv")

2. Target Preparation

The Risk Level column is converted into binary values:

Low  = 0
High = 1

3. Data Splitting

The data is divided into:

Training data

Validation data

Testing data

The split uses random_state=42 and stratification to preserve the class distribution.

4. Preprocessing Pipeline

Each model is trained inside a Scikit-learn pipeline containing:

SimpleImputer(strategy="mean")

StandardScaler()

A classification model

This keeps data preprocessing and model prediction together.

5. Models Compared

The training script tests several configurations of:

Random Forest Classifier

Decision Tree Classifier

Logistic Regression

6. Model Selection

The models are compared using a weighted score:

Overall Score =
    Accuracy × 0.20
  + Precision × 0.20
  + Recall × 0.35
  + F1-score × 0.25

Recall receives the highest weight because missing a high-risk pregnancy may be more serious than producing a false warning in an educational screening project.

The included saved pipeline currently uses:

RandomForestClassifier(
    n_estimators=50,
    max_depth=5,
    random_state=42
)

Installation

1. Clone the Repository

git clone YOUR_REPOSITORY_URL
cd Pregnancy_Risk_Prediction_System

Replace YOUR_REPOSITORY_URL with the link to your GitHub repository.

2. Create a Virtual Environment

python -m venv venv

3. Activate the Virtual Environment

Windows

venv\Scripts\activate

macOS or Linux

source venv/bin/activate

4. Install the Required Packages

pip install -r requirements.txt

Train the Model

Run:

python model_training_dataset_1.py

The script will:

Load dataset_1.csv

Remove rows with missing target values

Divide the data into training, validation, and testing sets

Apply missing-value imputation and feature scaling

Train multiple classification models

Compare accuracy, precision, recall, and F1-score

Select the model with the highest weighted validation score

Test the selected model

Save it as best_model_dataset_1.pkl

Run the Streamlit Web Application

Run:

streamlit run app.py

Streamlit will display a local address, usually:

http://localhost:8501

Open that address in a web browser.

Enter the requested information and click Predict Risk.

The application will display:

Calculated BMI

Converted glucose value in mg/dL

Predicted pregnancy-risk percentage

Low, medium, or high predicted risk

Run the Command-Line Program

Run:

python user_input.py

Enter each requested value in the terminal.

For yes-or-no questions, type:

yes

or:

no

The terminal program will display:

Calculated BMI

Predicted pregnancy-risk percentage

Example Input

Age: 30
Height: 5 feet 4 inches
Weight: 65 kg
Systolic blood pressure: 120
Diastolic blood pressure: 80
Blood sugar: 6.5 mmol/L
Body temperature: 98.6 °F
Heart rate: 82
Previous complications: No
Pre-existing diabetes: No
Gestational diabetes: No
Mental-health condition: No

The result depends on the patterns learned by the trained model.

Technologies Used

Python

Pandas

Scikit-learn

Streamlit

Joblib

Requirements

The project requires the following Python packages:

streamlit
pandas
scikit-learn
joblib

Common Problems

best_model_dataset_1.pkl Not Found

Train the model first:

python model_training_dataset_1.py

Make sure the model file is in the same folder as app.py and user_input.py.

streamlit Is Not Recognized

Install the project requirements:

pip install -r requirements.txt

You can also run Streamlit through Python:

python -m streamlit run app.py

Dataset File Not Found

Make sure dataset_1.csv is in the main project folder.

Incorrect Dataset Columns

The dataset must contain these columns:

Age
Systolic BP
Diastolic
BS
Body Temp
BMI
Previous Complications
Preexisting Diabetes
Gestational Diabetes
Mental Health
Heart Rate
Risk Level

Model Input Error

Do not change the feature names or their order without retraining the model.

Limitations

The project predicts statistical risk, not a clinical diagnosis.

Its performance depends on the quality and representativeness of the dataset.

The application does not use laboratory confirmation, medical imaging, physical examination, or a complete clinical history.

The displayed percentage is the classifier's estimated probability, not a medically validated risk score.

The current model predicts only two dataset classes: low risk and high risk.

The low, medium, and high interface labels are based on probability thresholds, not separate training classes.

Real clinical use would require external validation, fairness testing, calibration analysis, privacy protection, regulatory review, and supervision by medical professionals.

Future Improvements

Add cross-validation

Add model calibration analysis

Add confusion-matrix and model-comparison charts

Add feature-importance or SHAP explanations

Add input validation and clearer unit descriptions

Save prediction history securely

Add authentication

Deploy the application online

Test the model on an independent dataset

Evaluate bias across age and health-history groups

Add medically reviewed guidance and emergency-warning instructions


Contributors

Ragib Shahriar Majid — 2311007

Umme Habiba — 2311009

Arafat Howlader — 2311026

 medical condition. A high-risk or low-risk prediction may be incorrect. Consult a qualified healthcare professional for medical decisions.
