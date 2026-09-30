# PocketSmart AI — Smart Budget & Recommendation Assistant

PocketSmart AI is a FastAPI + Jinja2 web application based on the supplied project documentation.

## Features
- User registration/login/logout
- JWT authentication through secure HTTP-only cookie
- Home Interior Budget Planner
- Party Budget Planner
- Jewelry Budget Planner
- Optional outfit image upload for jewelry
- Gemini-powered recommendation generation
- Local mock/fallback recommendation catalog
- Recommendation history
- Responsive HTML/CSS/JavaScript frontend
- Simulated platform sourcing for Amazon, Flipkart, IKEA, Swiggy, Zomato and OYO

## Project structure
```text
PocketSmartAI/
├── app/
│   ├── main.py
│   ├── config.py
│   ├── database.py
│   ├── security.py
│   ├── models/
│   │   ├── __init__.py
│   │   └── schemas.py
│   ├── routes/
│   │   ├── __init__.py
│   │   ├── auth.py
│   │   ├── history.py
│   │   ├── pages.py
│   │   └── planners.py
│   ├── services/
│   │   ├── __init__.py
│   │   ├── gemini_service.py
│   │   └── mock_catalog.py
│   ├── static/
│   │   ├── css/style.css
│   │   └── js/app.js
│   └── templates/
│       ├── base.html
│       ├── index.html
│       ├── register.html
│       ├── login.html
│       ├── dashboard.html
│       ├── home_planner.html
│       ├── party_planner.html
│       ├── jewelry_planner.html
│       ├── history.html
│       └── 404.html
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

## Windows / VS Code setup

Open the project folder in VS Code.

### 1. Create virtual environment
PowerShell:
```powershell
py -m venv .venv
```

If `py` is unavailable:
```powershell
python -m venv .venv
```

### 2. Activate it
```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, run:
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

### 3. Install packages
```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 4. Create .env
Copy `.env.example` to `.env`.

For a first run, you can use:
```env
USE_MOCK_AI=true
```

This lets the full application run without a Gemini key.

For Gemini:
```env
GEMINI_API_KEY=YOUR_API_KEY_HERE
USE_MOCK_AI=false
GEMINI_MODEL=gemini-1.5-flash
```

Keep `.env` private and never commit it to GitHub.

### 5. Start the application
```powershell
python -m uvicorn app.main:app --reload
```

Open:
http://127.0.0.1:8000

FastAPI docs:
http://127.0.0.1:8000/docs

## Test flow
1. Register a user.
2. Login.
3. Open Home Planner and generate recommendations.
4. Open Party Planner and generate recommendations.
5. Open Jewelry Planner and optionally upload a JPG/PNG/WEBP image.
6. Open History to verify saved recommendation requests.
7. Visit `/docs` to test API endpoints directly.

## API endpoints
- POST `/api/register`
- POST `/api/login`
- POST `/api/logout`
- POST `/api/token`
- GET `/api/session-info`
- GET `/api/session-data`
- POST `/api/generate-home`
- POST `/api/generate-party`
- POST `/api/generate-jewelry`
- GET `/api/recommendations-details` is represented through planner responses/history in this implementation.
- GET `/api/history`
- DELETE `/api/history/{history_id}`

## Important note about product/platform data
The supplied documentation calls for Amazon, Flipkart, IKEA, Zomato, Swiggy and OYO data and explicitly permits mock/simulated sourcing during backend development. This implementation therefore does NOT scrape those sites and does NOT claim live price/availability. Replace `mock_catalog.py` with authorized partner APIs or another permitted data source when credentials are available.

## Troubleshooting
If `pip` is blocked by Windows policy, use:
```powershell
python -m pip install -r requirements.txt
```
instead of `pip install`.

If you see `ModuleNotFoundError`, confirm the terminal is opened at the PocketSmartAI project root and that `.venv` is activated.

If Gemini fails, set `USE_MOCK_AI=true` to confirm that the backend/frontend are working independently of the external AI service.
