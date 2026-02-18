# BravoBall

Monorepo for the BravoBall football training app — backend API and Flutter frontend.

## Project Structure

```
bravoball/
├── backend/          FastAPI + PostgreSQL API server
├── frontend/         Flutter mobile app (iOS, Android)
├── .github/workflows CI/CD pipelines
├── docker-compose.yml  Local dev environment
└── .env.example      Environment variable template
```

## Getting Started

### Prerequisites

- Python 3.9+
- Flutter SDK (stable channel)
- Docker & Docker Compose (optional, for containerized dev)
- PostgreSQL 15 (if running without Docker)

### Backend (with Docker)

```bash
# Copy env template and fill in values
cp .env.example backend/.env

# Start backend + database
docker compose up --build
```

The API will be available at `http://localhost:8000`.

### Backend (without Docker)

```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Copy env template and configure your database
cp ../.env.example .env

uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

### Frontend

```bash
cd frontend
flutter pub get
flutter run
```

## CI/CD

GitHub Actions workflows run automatically:

- **Backend CI** — Linting (flake8) and tests (pytest) on changes to `backend/`
- **Frontend CI** — Static analysis and tests on changes to `frontend/`

Workflows trigger on pushes and PRs to `main`, `develop`, and `staging` branches.

## Deployment

The backend is currently deployed on [Render](https://render.com). See `backend/render.yaml` for the service configuration.
