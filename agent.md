# AI-Powered Job Board - Developer Guidance & Roadmap

Welcome to the **AI-Powered Job Board** codebase. This project uses a modular, scalable architecture divided into a FastAPI backend and a React.js frontend.

This document contains comprehensive guidance, structural mapping, and step-by-step milestones to help you implement the complete application.

---

## 1. Project Prospects & Features

### Core Capabilities
1. **Authentication & Authorization**:
   - JWT-based authentication for Administrators and Candidates.
   - Guarded routes and role-based middleware access controls.
2. **Admin CRUD & Recruitment Pipeline**:
   - Recruiters can post, update, and manage job listings.
   - An interactive, glassmorphic pipeline interface tracks candidates across stages: `Applied` ➔ `Shortlisted` ➔ `Rejected`.
3. **Candidate Profile Setup**:
   - Candidate profile creation and management for skills, experience, and resume upload.
4. **Advanced Filtered Search**:
   - Real-time searching and filtering of jobs by keywords, location, and salary ranges.
5. **AI-Powered Match Engine**:
   - Candidates can enter natural language inputs describing their career goals or interests.
   - The system queries active jobs, evaluates similarity with the candidate's profile/resume, and returns a ranked list of job opportunities with a match percentage and a textual rationale explaining the score.
6. **Dashboard Analytics**:
   - Metrics reporting on applicant distributions, shortlist rates, and job posting counts.

---

## 2. Structural Mapping

We have configured the following folder structure to maintain high scalability:

### Backend Structure (`/backend`)
- `main.py`: Entrypoint initializing the FastAPI app, middlewares, and routers.
- `.env`: Database credentials and JWT secrets.
- `requirements.txt`: Python package requirements.
- `app/`
  - `config/`
    - `database.py`: SQLAlchemy engine setup and async db session logic.
    - `settings.py`: Environment configurations loader.
  - `models/`: SQLAlchemy ORM database models:
    - `user.py`: Model representing Users (credentials, email, role).
    - `job.py`: Model representing Job postings.
    - `profile.py`: Model representing Candidate profiles.
    - `application.py`: Model representing Job applications.
  - `schemas/`: Pydantic validation schemas:
    - `user_schema.py`, `job_schema.py`, `profile_schema.py`, `application_schema.py`.
  - `routes/`: Controller route definitions:
    - `auth_routes.py`, `job_routes.py`, `profile_routes.py`, `application_routes.py`, `dashboard_routes.py`, `ai_routes.py`.
  - `services/`: Encapsulated business logic layers:
    - `auth_service.py`, `job_service.py`, `profile_service.py`, `application_service.py`, `dashboard_service.py`, `ai_matching_service.py`.
  - `middleware/`
    - `auth_middleware.py`: Role and token authentication validation interceptors.
  - `utils/`
    - `jwt_handler.py`: Tokens generation and decoding helpers.
    - `response.py`: Standardized HTTP JSON payloads formatters.
- `tests/`
  - `test_auth.py`, `test_jobs.py`, `test_ai.py`.

### Frontend Structure (`/frontend`)
- `package.json`, `vite.config.js`: Bundler, dependencies, and path aliases.
- `public/`: Static public resources.
- `src/`
  - `assets/`: Global images and stylesheet graphics.
  - `api/`: API call handlers using Axios:
    - `authApi.js`, `jobApi.js`, `profileApi.js`, `applicationApi.js`, `aiApi.js`.
  - `components/`: Modular widgets:
    - `Navbar.jsx`, `Sidebar.jsx`, `JobCard.jsx`, `ApplicationCard.jsx`, `MatchCard.jsx`.
  - `pages/`: UI views grouped by authorization:
    - `auth/`: `Login.jsx`, `Register.jsx`.
    - `admin/`: `Dashboard.jsx`, `CreateJob.jsx`, `ManageJobs.jsx`, `Applications.jsx`.
    - `candidate/`: `Profile.jsx`, `Jobs.jsx`, `AIJobSearch.jsx`, `MyApplications.jsx`.
  - `routes/`
    - `AppRoutes.jsx`: Browser router path definitions.
  - `context/`
    - `AuthContext.jsx`: React state container for authorization credentials.
  - `utils/`
    - `token.js`: Browser localStorage token accessors.
  - `App.jsx`: Root UI router wrapper.
  - `main.jsx`: Dom renderer.

---

## 3. Step-by-Step Implementation Guide

Follow this sequence to build out the features:

### Step 1: Database Setup & Configuration
1. Initialize the async engine and sessionmaker in [database.py](file:///c:/Users/khade/JOBPORTEL/backend/app/config/database.py) using `create_async_engine` from `sqlalchemy.ext.asyncio`.
2. Configure settings parsing in [settings.py](file:///c:/Users/khade/JOBPORTEL/backend/app/config/settings.py).

### Step 2: Define SQLAlchemy Models
1. Define ORM models in [models/](file:///c:/Users/khade/JOBPORTEL/backend/app/models/).
2. Establish key relationships (e.g. applications linking profiles and jobs).

### Step 3: Implement Data Validation Schemas
1. Build request/response schema specifications in [schemas/](file:///c:/Users/khade/JOBPORTEL/backend/app/schemas/).

### Step 4: Implement JWT Security and Middlewares
1. Add generation/decoding logic in [utils/jwt_handler.py](file:///c:/Users/khade/JOBPORTEL/backend/app/utils/jwt_handler.py).
2. Wire up the extraction verification filter in [middleware/auth_middleware.py](file:///c:/Users/khade/JOBPORTEL/backend/app/middleware/auth_middleware.py).

### Step 5: Implement Services & Routes
1. Write logic inside [services/](file:///c:/Users/khade/JOBPORTEL/backend/app/services/) and bind them to corresponding routes in [routes/](file:///c:/Users/khade/JOBPORTEL/backend/app/routes/).
2. Wire routers into [main.py](file:///c:/Users/khade/JOBPORTEL/backend/main.py).

### Step 6: Setup React API Client and Routing
1. Mirror backend schemas in JS interface API functions inside [api/](file:///c:/Users/khade/JOBPORTEL/frontend/src/api/).
2. Setup authentication context in [context/AuthContext.jsx](file:///c:/Users/khade/JOBPORTEL/frontend/src/context/AuthContext.jsx).
3. Set up routes in [routes/AppRoutes.jsx](file:///c:/Users/khade/JOBPORTEL/frontend/src/routes/AppRoutes.jsx).

### Step 7: Build UI Views & Cards
1. Use glassmorphic card elements ([JobCard.jsx](file:///c:/Users/khade/JOBPORTEL/frontend/src/components/JobCard.jsx), [MatchCard.jsx](file:///c:/Users/khade/JOBPORTEL/frontend/src/components/MatchCard.jsx)) inside the recruiter dashboards ([Dashboard.jsx](file:///c:/Users/khade/JOBPORTEL/frontend/src/pages/admin/Dashboard.jsx)) and applicant search workspaces ([AIJobSearch.jsx](file:///c:/Users/khade/JOBPORTEL/frontend/src/pages/candidate/AIJobSearch.jsx)).
