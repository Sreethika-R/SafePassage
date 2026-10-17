# SafePassage

A Django web platform that helps tourists and night-shift workers in India stay safe. It gives live area-risk estimates, safe-route suggestions, shift check-ins with automatic escalation, and SOS alerts with email notifications.

Built during an AI/ML internship at Right Soft Options Institute, Kochi (Jan 2026 – Apr 2026).

## Features

**Tourist**
- Live area-risk estimate (LOW / MEDIUM / HIGH) with a per-signal breakdown, weather, and the nearest hospital and police station
- Safe-route planning with three route tiers (low, medium, high risk)
- Cultural safety guide, scam alerts and incident reporting
- Emergency phrase translation, nearby embassy information and emergency contacts
- SOS alerts with email notification and one-click acknowledgement links

**Night worker**
- Shift management with check-ins and check-outs
- Missed-check-in escalation: reminders every 2 minutes, then an automatic silent SOS after 8 minutes
- Safe-haven finder and safe-route planner
- SOS requires employer details and two emergency contacts

**Admin**
- Dashboard, user management (suspend or reactivate), SOS alert and incident handling
- Risk monitor, safe zones, analytics, cultural data
- Email broadcast to users

## How the risk score works

- **Live area risk** (`/api/predict-risk/`) is a weighted score from risk zones, crime data, incident reports, scam reports and weather. It adapts to whichever signals are available for a location.
- **Machine learning model:** `ml_pipeline.py` compares four classifiers (Random Forest, Gradient Boosting, Logistic Regression, SVM) using grid search and 5-fold cross-validation, then saves the best one (currently Gradient Boosting). It is used by the public prediction form (`/predict/`).

## Tech stack

Python, Django, SQLite, scikit-learn, pandas, joblib, HTML/CSS/JavaScript, Bootstrap

## Access control

Four roles are defined (Tourist, Worker, Employer, Admin). Login and role checks restrict protected pages and APIs. A request from the wrong role gets a 403 response on APIs or an "unauthorized" page on dashboards. Admin accounts cannot be created through public registration.

## Run it locally

python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
cd safepassage_backend
python manage.py migrate
python manage.py runserver

Then open http://127.0.0.1:8000/

Email alerts need SMTP settings. Copy `safepassage_backend/.env.example` to `safepassage_backend/.env` and fill in the email values. The app runs without them, but emails will not be sent.

## Run the tests

cd safepassage_backend
python manage.py test

Result at the time of writing: 79 tests, all passing.

## Retrain the model (optional)

From the repository root:

python ml_pipeline.py

## Limitations

- The ML model was trained on 29 records derived from NCRB crime data, so its accuracy figures are indicative only.
- The live area score is rule-based. Connecting the trained model to it is a planned next step.
- Email alerts work only when SMTP is configured, and the project runs on SQLite with `DEBUG=True`, so it is a development setup, not a production deployment.
- The risk labels (Low/Medium/High) are generated from a score and the test set has only 6 samples, so the model's 100% accuracy is not evidence of real-world performance.
- The risk labels come from a formula dominated by total crime count, so the trained model mostly learns that one feature.
- One input feature (Tourist_Risk_Factor) is simulated with random values, so retraining gives slightly different results each time.

## Author

Sreethika R