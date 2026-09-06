# SafePassage 🛡️



An AI-driven personal safety platform designed for tourists and night-shift workers, combining real-time risk analysis, location tracking, and emergency response tools in a single web application.



## Overview



SafePassage was built during an AI/ML internship, addressing a real safety gap: tourists and night workers often lack accessible, data-driven tools to assess area risk and get help quickly in an emergency. The platform offers two tailored operating modes — **Tourist** and **Night Worker** — each with dashboards, alerts, and workflows suited to that user's specific safety needs.



I conceived the product, defined the system architecture and AI/ML approach (crime-data-driven risk scoring, dual operating modes, RBAC-based access control), and directed the implementation, reviewing progress and functionality throughout development.



## Key Features



- **AI-Driven Risk Analysis Engine** — combines rule-based scoring with a trained Random Forest model on NCRB crime data to assess area risk in real time

- **Dual Operating Modes** — separate, purpose-built experiences for tourists (safe routes, scam alerts, cultural guides) and night workers (shift check-ins, safe havens, route planning)

- **Emergency SOS System** — one-tap SOS alerts with automated email notifications to emergency contacts

- **Role-Based Access Control (RBAC)** — secure, tiered access across user types and an admin control panel

- **Admin Dashboard** — analytics, incident monitoring, risk zone management, and system logs

- **Location-Based Safety Tools** — safe route suggestions, risk zone mapping, and safe haven discovery



## Tech Stack



- **Backend:** Python, Django

- **Machine Learning:** scikit-learn (Random Forest), pandas, NCRB crime datasets

- **Database:** SQLite

- **Frontend:** Django Templates, HTML/CSS, JavaScript

- **Other:** REST-style internal APIs, SMTP email integration for alerts



## Project Structure



safepassage/

├── ml_pipeline.py # ML training pipeline (risk model)

├── ml-models # Trained model artifacts, plots, metrics

├── dataset # NCRB crime datasets used for training

├── requirements.txt

└── safepassage_backend # Django project

├── safety # Core app: models, views, risk engine, ML integration

├── templates # Tourist, worker, and admin UI templates

└── static # CSS, images





## Setup



```bash

git clone https://github.com/Sr-2525/SafePassage.git

cd SafePassage/safepassage_backend

pip install -r ../requirements.txt

cp .env.example .env   # then fill in your own email credentials

python manage.py migrate

python manage.py runserver

```



## Notes



This project was built as part of a company-run internship program, where implementation support was provided by a developer assigned through the program. The core concept, system design, risk-analysis approach, and technical direction throughout development were mine.

