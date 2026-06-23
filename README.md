# TruthLab

TruthLab is a fake-news verification web application. It combines a React frontend with a Flask API that can classify submitted news text or article URLs using a saved scikit-learn model and TF-IDF vectorizer.

## Features

- User signup and login with JWT-based authentication.
- Optional Google OAuth login flow.
- News verification from direct text or a URL.
- Verification history for authenticated users.
- FAQ question submission.
- Issue report submission.
- MongoDB-backed persistence for users, verification history, FAQ questions, and reports.

## Tech Stack

### Frontend

- React 19
- Vite
- React Router
- Tailwind CSS
- Lucide React icons

### Backend

- Python Flask
- Flask-JWT-Extended
- Flask-Bcrypt
- Flask-CORS
- PyMongo
- scikit-learn and joblib
- BeautifulSoup and requests for URL article extraction

## Project Structure

```text
TruthLab/
|-- backend/
|   |-- app.py
|   |-- models.py
|   |-- requirements.txt
|   |-- middleware/
|   |-- model/
|   |   |-- fake_news_model.pkl
|   |   `-- tfidf_vectorizer.pkl
|   `-- routes/
`-- frontend/
    |-- package.json
    |-- vite.config.js
    |-- public/
    `-- src/
```

## Prerequisites

- Node.js and npm
- Python 3.10 or newer
- MongoDB Atlas database or a compatible MongoDB instance

## Backend Setup

From the project root:

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Create a `.env` file in `backend/`:

```env
MONGO_URI=mongodb+srv://<user>:<password>@<cluster>/<database>?retryWrites=true&w=majority
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_REDIRECT_URI=http://127.0.0.1:5000/auth/google/callback
FRONTEND_URL=http://localhost:5173
```

Run the API:

```powershell
python app.py
```

The backend runs at:

```text
http://127.0.0.1:5000
```

## Frontend Setup

Open a second terminal from the project root:

```powershell
cd frontend
npm install
npm run dev
```

The Vite development server usually runs at:

```text
http://localhost:5173
```

## API Endpoints

### Auth

- `POST /auth/signup`
- `POST /auth/login`
- `GET /auth/google/login`
- `GET /auth/google/callback`

### Verification

- `GET /verify/health`
- `POST /verify/predict`
- `GET /verify/history`

`POST /verify/predict` accepts either:

```json
{
  "text": "Article or headline text"
}
```

or:

```json
{
  "url": "https://example.com/news-article"
}
```

### FAQ

- `POST /faq/submit-question`

### Reports

- `POST /report/submit-report`

## Useful Commands

Frontend:

```powershell
npm run dev
npm run build
npm run lint
npm run preview
```

Backend:

```powershell
python app.py
```

## Notes for Maintainers

- `backend/models.py` imports `python-dotenv`, but `python-dotenv` is not currently listed in `backend/requirements.txt`.
- `backend/routes/faq_routes.py` and `backend/routes/report_routes.py` contain hardcoded MongoDB connection strings. Move these to environment variables before sharing or deploying the project.
- `backend/routes/verify_routes.py` imports `utils.text_cleaner`, but no `backend/utils/text_cleaner.py` file is currently present in the repository.
- `backend/routes/admin_routes.py` imports `model.user_model`, but that module is not currently present in the repository.
- `frontend/src/App.js` uses `PrivateRoute`, but it is not currently imported or defined.
- The login, signup, and verification form UI currently appears to be mostly static; some frontend components do not yet call the backend API.

## Watch Demo
[TruthLab - Project Demo](https://www.linkedin.com/posts/kaveesha-sewmini-6862142b7_computerscience-miniproject-artificialintelligence-activity-7444394599189680128-V8ZU?utm_source=share&utm_medium=member_desktop&rcm=ACoAAEwHN8YBMimIh3vAIEjxbD3AuPRmZysgmZM)


