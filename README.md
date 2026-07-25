# CreditShield: Credit Card Approval Prediction System

CreditShield is a machine learning platform designed to automate credit risk assessment and credit card application decisions. By leveraging historical applicant demographics and payment records, the platform processes raw applicant features, evaluates credit risks, and predicts approval decisions.

This project implements the full pipeline: data ingestion, feature engineering, class imbalance mitigation, training of four classification algorithms (**Logistic Regression, Decision Tree, Random Forest, and XGBoost**), performance analysis, and an interactive Flask web application.

---

## Technical Features

1. **Exploratory Data Analysis (EDA) Dashboard**: Dynamic visual indicators (built on Chart.js) analyzing applicant distributions by gender, education level, income brackets, and source types.
2. **Real-time Screening (Scenario 1 & 3)**: An interactive prediction portal where analysts or customers can input a profile, select an algorithm (e.g. XGBoost, Random Forest), and receive an instant approval decision with confidence scores.
3. **Batch Screening & Compliance (Scenario 2)**: A secure file drag-and-drop tool to batch-evaluate hundreds of applicants concurrently. Outputs a screened, compliance-ready CSV detailing decisions and risk levels.
4. **Classification Leaderboard**: Interactive leaderboard ranking the four models by F1-Score (correcting for extreme class imbalance in banking data) alongside ROC curves and confusion matrices.
5. **IBM Watson ML Readiness**: Dedicated scripting and authentication templates to register the local pipeline and host it on IBM Cloud.

---

## Directory Structure

```
credit_card_approval_prediction/
├── data/                      # Raw CSV datasets
├── models/                    # Serialized joblib pipelines and metrics
├── static/
│   ├── css/
│   │   └── style.css          # Dark-themed financial UI styles
│   ├── js/
│   │   └── main.js           # Range sliders, dropzone, and gauges logic
│   └── img/                   # Model performance plots and matrices
├── templates/
│   ├── base.html              # Shell layout with sidebar navigation
│   ├── index.html             # Homepage scenario overview
│   ├── predict.html           # Real-time screening inputs & results gauge
│   ├── batch.html             # CSV upload drag-and-drop & screened previews
│   ├── dashboard.html         # Demographics and approval rate charts
│   └── comparison.html        # Models metrics and leaderboard plots
├── app.py                     # Flask web server
├── train.py                   # Preprocessing and ML model training script
├── download_data.py           # Auto-downloader for Kaggle dataset files
├── deploy_watson.py           # IBM Watson ML deployment pipeline script
├── requirements.txt           # Python environment packages list
└── README.md                  # Project documentation guide
```

---

## Installation & Running

### 1. Setup Environment
Navigate to the project directory and install dependencies:
```bash
pip install -r requirements.txt
```

### 2. Download Datasets
Download the Kaggle `application_record.csv` and `credit_record.csv` datasets from our repository fallbacks:
```bash
python download_data.py
```

### 3. Run Preprocessing & Model Training
Execute the training script to preprocess the data, handle class imbalance, train all four models, and save evaluation metrics and plots:
```bash
python train.py
```

### 4. Start the Web Server
Launch the Flask development server:
```bash
python app.py
```
Open a browser and navigate to: `http://127.0.0.1:5000`

---

## IBM Watson Machine Learning Deployment

To host your trained XGBoost model on IBM Cloud:
1. Make sure the Watson Machine Learning client is installed: `pip install ibm-watson-machine-learning`.
2. Open `deploy_watson.py` and input your credentials:
   - `IBM_CLOUD_API_KEY`
   - `IBM_CLOUD_SPACE_ID` (Deployment space identifier)
3. Run the script:
   ```bash
   python deploy_watson.py
   ```
4. Copy the resulting `Scoring Endpoint` and plug it into your server code to run inference via IBM Cloud.
