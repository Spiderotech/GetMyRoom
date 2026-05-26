# Development Guide

## Prerequisites

Install:

- Node.js
- npm
- MongoDB locally or MongoDB Atlas access
- Git

Optional:

- AWS account for S3 upload testing
- SMTP/email provider credentials for inquiry email testing

## Install Dependencies

Backend:

```bash
cd BACKEND
npm install
```

Frontend:

```bash
cd FRONTEND
npm install
```

## Run Locally

Backend:

```bash
cd BACKEND
npm start
```

Frontend:

```bash
cd FRONTEND
npm run dev
```

Open:

```text
http://localhost:5173
```

## Build Frontend

```bash
cd FRONTEND
npm run build
```

Preview production build:

```bash
cd FRONTEND
npm run preview
```

## Lint Frontend

```bash
cd FRONTEND
npm run lint
```

## Backend Development Notes

The backend script is:

```json
{
  "start": "nodemon app.js"
}
```

Because `nodemon` is listed in dependencies, `npm start` restarts the API when backend files change.

Recommended improvements:

- Add a separate production start script using `node app.js`.
- Add a `dev` script using `nodemon app.js`.
- Add centralized error handling middleware.
- Add request validation.
- Add authentication middleware to protected routes.
- Add unit/integration tests.

## Frontend Development Notes

The frontend is a Vite app. Most user-facing code is under:

```text
FRONTEND/src/Pages/
FRONTEND/src/Components/
```

Admin code is under:

```text
FRONTEND/src/Components/admin/
```

API clients are under:

```text
FRONTEND/src/Components/Utils/
FRONTEND/src/Components/admin/Utils/
```

Recommended improvements:

- Move API base URLs to `VITE_API_BASE_URL`.
- Fix hard-coded production API URLs for local development.
- Remove unused dependencies where possible.
- Add route guards for authenticated user/admin pages.
- Add loading and error states consistently.

## Suggested Git Workflow

The root folder is not currently a git repository. After creating a repository:

```bash
git checkout -b feature/<feature-name>
```

Before committing:

```bash
cd FRONTEND
npm run lint
npm run build
```

Commit:

```bash
git add .
git commit -m "Describe the change"
```

## Development Checklist

- [ ] Create `.env` files locally.
- [ ] Start MongoDB or configure Atlas.
- [ ] Run backend on `PORT=3000`.
- [ ] Run frontend on Vite dev server.
- [ ] Confirm frontend API base URL points to local backend.
- [ ] Test register/login.
- [ ] Test add property.
- [ ] Test list/detail pages.
- [ ] Test save property.
- [ ] Test admin login and approval.
- [ ] Test email and upload integrations after credentials are created.
