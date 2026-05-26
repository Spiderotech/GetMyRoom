# GetMyRoom

GetMyRoom is a full-stack property listing platform with separate frontend and backend applications. Users can register, log in, list properties, browse available properties, save properties, manage their profile, and send property inquiries. Admin users can log in, view users, review listed and unlisted properties, and approve property listings.

The project is currently not hosted. The current workspace is also not initialized as a git repository, so no git remote URL is configured locally yet. Add the final repository URL here after the repo is created:

```text
Git repository: TBD
```

## Applications

| App | Path | Stack | Purpose |
| --- | --- | --- | --- |
| Backend | `BACKEND/` | Node.js, Express, MongoDB, Mongoose | REST API, authentication, property management, admin APIs, S3 signed URL generation, email sending |
| Frontend | `FRONTEND/` | React, TypeScript, Vite, Tailwind CSS, Redux Toolkit | User website and admin dashboard |

## Current Hosting Status

- Frontend: not hosted.
- Backend API: not hosted.
- Database: production database should be provisioned before launch.
- S3 bucket: not created for this environment yet.
- Cloud credentials: not created or configured for development/production yet.
- Domain: not connected to the current deployment.

Some frontend constants currently point to `https://getmyroom.co.uk/api/v1/...`. Treat those as old or planned production URLs until hosting is completed.

## Quick Start

Install and run the backend:

```bash
cd BACKEND
npm install
npm start
```

Install and run the frontend:

```bash
cd FRONTEND
npm install
npm run dev
```

Default local URLs:

- Frontend: `http://localhost:5173`
- Backend: controlled by `BACKEND/.env` value `PORT`, commonly `3000`

## Required Environment Variables

Create `BACKEND/.env` before running the API:

```env
PORT=3000
MONGO_URI=mongodb://localhost:27017/getmyroom
ACESS_TOKEN_SCERET=replace_with_access_token_secret
REFRESH_TOKEN_SECRET=replace_with_refresh_token_secret
S3_ACESS_KEY=replace_when_s3_is_created
S3_SECRET_KEY=replace_when_s3_is_created
EMAIL=replace_with_sender_email
PASSWORD=replace_with_email_app_password
```

Important: the current backend config contains hard-coded database and email values. Move all secrets and environment-specific values into `.env` before using this project for development, staging, or production.

## Main Scripts

Backend:

```bash
npm start
```

Frontend:

```bash
npm run dev
npm run build
npm run preview
npm run lint
```

## Documentation

Detailed documentation is available in `docs/`:

- [Project Documentation](docs/PROJECT_DOCUMENTATION.md)
- [Hosting Documentation](docs/HOSTING_DOCUMENTATION.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Folder Structure](docs/FOLDER_STRUCTURE.md)
- [API Documentation](docs/API_DOCUMENTATION.md)
- [Environment Setup](docs/ENVIRONMENT.md)
- [Database Documentation](docs/DATABASE.md)
- [Development Guide](docs/DEVELOPMENT.md)

## Before Production

- Initialize the root git repository and add the remote URL.
- Remove hard-coded secrets from source code.
- Create separate development and production environment files.
- Provision MongoDB for production.
- Create the S3 bucket and IAM credentials.
- Configure frontend API base URLs through environment variables.
- Add authentication middleware and route protection where required.
- Add validation, error handling, and automated tests.
- Deploy backend and frontend, then connect the production domain.
