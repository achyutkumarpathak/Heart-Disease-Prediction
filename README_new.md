# ❤️ Heart Disease Prediction using Machine Learning

A machine learning project that predicts the risk of heart disease from patient health information. The project includes exploratory data analysis, data cleaning, feature encoding, feature scaling, model comparison, and a **Streamlit web application** for making predictions using a saved KNN model.

## 📌 Project Overview

Heart disease is a major health concern, and machine learning can be used to identify patterns in patient data that may help classify whether a person is at risk of heart disease.

In this project, several classification algorithms are trained and evaluated. A **K-Nearest Neighbors (KNN)** model is saved and integrated into a Streamlit application so that users can enter patient information and receive a heart-disease risk prediction.

> **Important:** This project is intended for educational purposes and is not a medical diagnostic tool.

## 🎯 Problem Statement

Build a binary classification model that predicts whether a patient is likely to have heart disease based on clinical and demographic features.

### Target Variable

`HeartDisease`

- `0` → No heart disease
- `1` → Heart disease

## 📊 Dataset

The project uses a dataset named `heart.csv`.

The dataset contains the following original features:

| Feature | Description |
|---|---|
| `Age` | Age of the patient |
| `Sex` | Sex of the patient |
| `ChestPainType` | Type of chest pain |
| `RestingBP` | Resting blood pressure |
| `Cholesterol` | Cholesterol level |
| `FastingBS` | Fasting blood sugar indicator |
| `RestingECG` | Resting ECG result |
| `MaxHR` | Maximum heart rate achieved |
| `ExerciseAngina` | Exercise-induced angina |
| `Oldpeak` | ST depression |
| `ST_Slope` | Slope of the peak exercise ST segment |
| `HeartDisease` | Target variable |

## 🔍 Exploratory Data Analysis

The notebook performs several EDA steps to understand the dataset and relationships between features and the target.

### Data inspection

The project checks:

- Dataset structure
- Column names
- Descriptive statistics
- Duplicate records
- Missing values
- Target-class distribution

### Visualizations

The notebook uses:

- Histograms with KDE
- Count plots
- Boxplots
- Violin plots
- Correlation heatmap

Examples include examining age, resting blood pressure, cholesterol, maximum heart rate, sex, chest pain type, fasting blood sugar, and their relationship with heart disease.

## 🧹 Data Cleaning

During the analysis, zero values were found in `Cholesterol` and `RestingBP`.

Because zero is not a meaningful measurement for these clinical variables, the project replaces zero values with the mean of their non-zero observations.

### Cholesterol

The mean of non-zero cholesterol values is calculated and used to replace zero values. The resulting values are rounded to two decimal places.

### Resting Blood Pressure

The mean of non-zero resting blood pressure values is calculated and used to replace zero values. The resulting values are rounded to two decimal places.

## 🔄 Feature Engineering & Preprocessing

### 1. One-Hot Encoding

Categorical features are converted into numerical features using:

```python
pd.get_dummies(df, drop_first=True)
```

### 2. Integer Conversion

The encoded dataframe is converted to integer type.

### 3. Feature Scaling

The following numerical features are standardized using `StandardScaler`:

```text
Age
RestingBP
Cholesterol
MaxHR
Oldpeak
```

The fitted scaler is saved as `scaler.pkl`.

### 4. Train-Test Split

The dataset is split into:

- **80% training data**
- **20% testing data**

using `random_state=42`.

## 🤖 Machine Learning Models

The project compares five classification algorithms:

1. Logistic Regression
2. K-Nearest Neighbors (KNN)
3. Gaussian Naive Bayes
4. Decision Tree
5. Support Vector Machine (SVM)

The models are evaluated using **Accuracy** and **F1 Score**.

## 📈 Model Performance

The recorded notebook results are:

| Model | Accuracy | F1 Score |

| Logistic Regression | **85.87%** | **87.38%** |
| KNN | 83.70% | 85.58% |
| Naive Bayes | 84.78% | 86.14% |
| Decision Tree | 77.72% | 79.60% |
| SVM | 84.78% | 86.79% |

### 🏆 Best Recorded Model

Based on the notebook's evaluation results, **Logistic Regression** achieved the highest recorded accuracy and F1 score.

However, the project saves and deploys the **KNN model** through the Streamlit application. Therefore:

- **Best model in the recorded comparison:** Logistic Regression
- **Model used by the current application:** KNN

This distinction is documented so the README accurately represents the supplied project.

## 💾 Saved Machine Learning Files

The notebook saves:

```text
KNN_heart.pkl
scaler.pkl
column.pkl
```

- `KNN_heart.pkl` → trained KNN classification model
- `scaler.pkl` → fitted `StandardScaler`
- `column.pkl` → expected feature-column order used by the trained model

The saved feature columns are:

```text
Age
RestingBP
Cholesterol
FastingBS
MaxHR
Oldpeak
Sex_M
ChestPainType_ATA
ChestPainType_NAP
ChestPainType_TA
RestingECG_Normal
RestingECG_ST
ExerciseAngina_Y
ST_Slope_Flat
ST_Slope_Up
```

## 🖥️ Streamlit Application

The project includes a Streamlit application in `app.py`.

The application loads the saved model, scaler, and expected columns before accepting user input. It then creates a one-row DataFrame, adds missing encoded columns as zero, restores the expected column order, scales the numerical features, and sends the processed input to the KNN model.

The current application provides inputs for Age, Sex, Chest Pain Type, Resting Blood Pressure, Cholesterol, Fasting Blood Sugar, Resting ECG, Maximum Heart Rate, Exercise-Induced Angina, Oldpeak, and ST Slope.

## 🔮 Prediction Workflow

```text
User enters patient information
            ↓
Create raw input dictionary
            ↓
Convert input into DataFrame
            ↓
Add missing encoded columns with 0
            ↓
Reorder columns using column.pkl
            ↓
Scale numerical features using scaler.pkl
            ↓
Pass processed data to KNN model
            ↓
Generate prediction
            ↓
Display risk result
```

If the model predicts `1`, the application displays **High Risk of Heart Disease**. If it predicts `0`, it displays **Low Risk of Heart Disease**.

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Joblib
- Streamlit

## 📂 Project Structure

```text
Heart-Disease-Prediction/
│
├── Heart_Disease_prediction.ipynb
├── app.py
├── heart.csv
├── KNN_heart.pkl
├── scaler.pkl
├── column.pkl
├── requirements.txt
└── README.md
```

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd Heart-Disease-Prediction
```

### 2. Create a virtual environment

Windows:

```bash
python -m venv venv
```

PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn joblib streamlit
```

Or, if `requirements.txt` is included:

```bash
pip install -r requirements.txt
```

## ▶️ Run the Streamlit Application

Make sure these files are available in the project directory:

```text
app.py
KNN_heart.pkl
scaler.pkl
column.pkl
```

Run:

```bash
streamlit run app.py
```

Then open the local Streamlit URL shown in the terminal, normally:

```text
http://localhost:8501
```

## 📓 Run the Jupyter Notebook

```bash
jupyter notebook
```

Open the heart-disease notebook and make sure `heart.csv` is available in the notebook's working directory.

## 🧠 Key Concepts Demonstrated

- Exploratory Data Analysis
- Data cleaning
- Handling invalid zero values
- One-hot encoding
- Feature scaling
- Train-test splitting
- Classification algorithms
- Model comparison
- Accuracy and F1-score evaluation
- Model serialization with Joblib
- Maintaining feature-column order during inference
- Reusing a fitted scaler during prediction
- Building an interactive ML application with Streamlit

## 🔮 Future Improvements

- Hyperparameter tuning for KNN
- Cross-validation
- Compare additional classification algorithms
- Select the deployment model based on validation performance
- Add precision, recall, ROC-AUC and confusion matrix
- Use a complete `Pipeline` / `ColumnTransformer`
- Improve Streamlit UI/UX
- Display prediction probability/confidence
- Add stronger input validation and error handling
- Deploy the Streamlit application online

## ⚠️ Disclaimer

This project is created for **educational and machine-learning demonstration purposes only**. The predictions should not be interpreted as a medical diagnosis or professional medical advice. Consult qualified healthcare professionals for medical decisions.

## 👨‍💻 Author

**Achyut Kumar Pathak**  
BCA — Artificial Intelligence & Deep Learning
