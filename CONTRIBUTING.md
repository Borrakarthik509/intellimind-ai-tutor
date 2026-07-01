# Contributing to INTELLMIND

First off, thank you for considering contributing to INTELLMIND! 

## Local Setup

The project consists of a Python FastAPI backend and a Vanilla JS frontend. You will need to run both concurrently for local development.

### Backend Setup (Python/FastAPI)
1. Ensure you have Python 3.10+ installed.
2. Navigate to the `backend/` directory.
3. Install dependencies: `pip install -r requirements.txt`.
4. Copy `.env.example` to `.env` and fill in the required keys.
   - **Important:** Make sure your `ALLOWED_ORIGINS` environment variable includes `http://127.0.0.1:5501` to allow requests from the local Live Server.
5. Start the server: `uvicorn main:app --reload --port 8000`

### Frontend Setup (Live Server)
1. The frontend is purely static HTML/CSS/JS and does not require a build step (Node.js/npm is not required).
2. Open the `frontend/` directory in VS Code.
3. Install the **Live Server** extension.
4. Click "Go Live" at the bottom right of VS Code to start the server on `http://127.0.0.1:5501`.

## Dual Supabase Architecture

This project uses a dual Supabase project architecture for enhanced security and separation of concerns:
1. **Auth DB**: Handles user authentication (JWTs, `login_logs`).
2. **Data DB**: Stores application data (`chat_summary`, `study_plans`, `plan_tasks`).

To contribute effectively, you will need two Supabase projects configured in your local environment. Provide the corresponding URLs and keys in both your backend `.env` and frontend `env.js` (publishable keys only for the frontend!).

## Contribution Areas

We welcome contributions across the stack. Here are a few key areas where you can make an immediate impact:

- **Intent Detector (`backend/app/services/intent.py`)**: The intent detector relies on keyword patterns (currently 200+). Adding new educational intents or refining existing patterns can greatly improve AI data fetching efficiency.
- **Offline Fallback Generator (`backend/app/routes/roadmap.py`)**: Improve the rule-based offline fallback plan generator used when the Gemini API is unavailable or rate-limited.
- **Frontend Pages**: Add new feature pages or improve the UI/UX of the existing responsive architecture.
