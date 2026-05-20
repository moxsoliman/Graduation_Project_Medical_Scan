[disease_plus_covid_v_4_readme.md](https://github.com/user-attachments/files/28074117/disease_plus_covid_v_4_readme.md)
# Disease Plus COVID Prediction System

A full-stack web application that predicts diseases based on user-selected symptoms and provides a dedicated COVID-19 risk assessment module.

This project combines:

- **General Disease Prediction** using a trained TensorFlow/Keras neural network.
- **COVID-19 Risk Assessment** using a machine learning model with symptom and vital-sign analysis.
- **User Authentication** with SQLite.
- **FastAPI Backend** for API endpoints.
- **HTML/CSS/JavaScript Frontend** with a multi-step user interface.

---

## Features

### General Disease Prediction

- Predicts diseases from selected symptoms.
- Uses a trained deep learning model (`disease_prediction_model.keras`).
- Supports a large symptom catalog.

### COVID-19 Assessment

- Evaluates current COVID-19 probability.
- Estimates future exposure risk based on:
  - Recent travel
  - Contact with confirmed cases
  - Symptom onset timing
- Uses:
  - Age
  - Gender
  - Temperature
  - Blood pressure
  - Oxygen saturation (SpO2)
  - Symptom indicators

### User Authentication

- User registration
- Login system
- Password hashing with SHA-256
- SQLite database storage

### Frontend Workflow

- Start page
- Symptom selection
- Processing page
- Results page
- Dedicated COVID-19 assessment pages

---

## Project Structure

```text
Disease_Plus_COVID/
│
├── backend/
│   ├── main.py                     # FastAPI application
│   ├── covid_model.py              # COVID model utilities
│   ├── requirements.txt            # Python dependencies
│   ├── users.db                    # SQLite database
│   │
│   ├── models/
│   │   └── covid_v2.joblib         # Trained COVID model
│   │
│   ├── data/
│   │   ├── covid_merged_real.csv
│   │   ├── covid_merged_training_data.csv
│   │   └── raw/
│   │       ├── israel_corona_tested_individuals.xlsx
│   │       └── physionet_subject_description.csv
│   │
│   └── tools/
│       ├── train_covid_v2.py
│       └── merge_real_covid_datasets.py
│
├── frontend/
│   ├── assets/
│   │   └── symptom_catalog.json
│   │
│   ├── login_page/
│   ├── step1_start/
│   ├── step2_input/
│   ├── step3_processing/
│   ├── step4_result/
│   ├── covid_check_input/
│   └── covid_check_result/
│
├── model/
│   ├── disease_prediction_model.keras
│   ├── training_data.csv
│   ├── model_train.py
│   ├── predict.py
│   └── old_disease_prediction_model.keras
│
└── README.md
```

---

## Technologies Used

### Backend

- Python 3.10+
- FastAPI
- TensorFlow / Keras
- Scikit-learn
- Pandas
- NumPy
- Joblib
- SQLite
- Uvicorn

### Frontend

- HTML5
- CSS3
- JavaScript (Vanilla JS)

### Machine Learning

- Neural Networks (TensorFlow/Keras)
- Traditional ML models (Scikit-learn)

---

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/disease-plus-covid-prediction.git
cd disease-plus-covid-prediction
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

### 3. Activate the Virtual Environment

#### Windows

```bash
venv\Scripts\activate
```

#### Linux / macOS

```bash
source venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -r backend/requirements.txt
```

---

## Running the Backend

From the project root:

```bash
cd backend
uvicorn main:app --reload
```

The API will be available at:

- `http://127.0.0.1:8000`
- Swagger Docs: `http://127.0.0.1:8000/docs`
- ReDoc: `http://127.0.0.1:8000/redoc`

---

## Running the Frontend

Open any frontend page directly in the browser, or use a local web server.

Recommended using Python:

```bash
cd frontend
python -m http.server 5500
```

Then open:

```text
http://localhost:5500/login_page/index.html
```

---

## API Endpoints

### Root

| Method | Endpoint | Description |
|------:|----------|-------------|
| GET | `/` | API health check |

### Authentication

| Method | Endpoint | Description |
|------:|----------|-------------|
| POST | `/register` | Create a new user |
| POST | `/login` | Authenticate an existing user |

### Disease Prediction

| Method | Endpoint | Description |
|------:|----------|-------------|
| POST | `/predict` | Predict disease from symptoms |

### COVID Assessment

| Method | Endpoint | Description |
|------:|----------|-------------|
| POST | `/covid/assess` | Assess current and future COVID risk |

### Debug

| Method | Endpoint | Description |
|------:|----------|-------------|
| GET | `/debug_model` | Check model loading status |

---

## Example Requests

### Disease Prediction

```json
POST /predict
{
  "symptoms": [
    "itching",
    "skin_rash",
    "nodal_skin_eruptions"
  ]
}
```

### COVID Assessment

```json
POST /covid/assess
{
  "age": 30,
  "gender": "male",
  "has_high_temp": true,
  "temperature_c": 38.5,
  "spo2": 96,
  "symptom_onset_days": 2,
  "recent_travel": false,
  "contact_confirmed": true,
  "days_since_contact": 3,
  "symptoms": {
    "fever": true,
    "dry_cough": true,
    "fatigue": true,
    "loss_smell": true
  }
}
```

---

## Machine Learning Models

### Disease Prediction Model

- File: `model/disease_prediction_model.keras`
- Trained using `model/training_data.csv`
- Training script: `model/model_train.py`

### COVID Model

- File: `backend/models/covid_v2.joblib`
- Training script: `backend/tools/train_covid_v2.py`
- Dataset merging script: `backend/tools/merge_real_covid_datasets.py`

---

## Authentication Details

- User credentials are stored in `backend/users.db`.
- Passwords are hashed using SHA-256.
- For production, it is recommended to replace SHA-256 with:
  - `bcrypt`
  - `argon2`

---

## Data Sources

The project uses multiple datasets, including:

- Symptom-to-disease training data
- Israeli COVID testing data
- PhysioNet subject descriptions

These are merged and processed to create a more realistic COVID-19 assessment model.

---

## Notes and Limitations

- This project is intended for **educational and research purposes only**.
- Predictions are **not medical diagnoses**.
- The authentication system is basic and should not be used as-is in production.
- The COVID model provides probabilistic risk estimates, not confirmed infection status.

---

## Future Improvements

- JWT authentication
- Password hashing with bcrypt/argon2
- Docker deployment
- Database migration to PostgreSQL
- Model confidence explanations
- Responsive mobile design
- Additional disease categories

---

## Screens Included

- Login Page
- Disease Prediction Workflow
- COVID Assessment Input
- COVID Assessment Results

---

## License

This project is provided for educational purposes. You may modify and use it freely for academic and non-commercial work.

---

## Author

Developed as a machine learning and web development project integrating:

- Artificial Intelligence
- Medical Data Analysis
- FastAPI Backend Development
- Frontend Web Design

---

## Disclaimer

This software does not replace professional medical advice, diagnosis, or treatment. Always consult a qualified healthcare provider regarding medical concerns.

