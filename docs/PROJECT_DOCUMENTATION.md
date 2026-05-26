# Project Documentation

## Project Overview

GetMyRoom is a property listing platform built as two separate applications:

- `BACKEND/`: Express API for users, properties, admin features, email, database access, and file upload URL generation.
- `FRONTEND/`: React/Vite client for public users and admin users.

The product supports:

- User email registration with OTP verification.
- User login and Google login.
- User profile update.
- Property listing creation.
- Property browsing and filtering by location/type.
- Single property details.
- Saved property list.
- Property inquiry emails.
- Admin login.
- Admin user listing.
- Admin listed/unlisted property review.
- Admin property approval.

## Git Repository

The project source code is maintained in a GitHub repository.

Repository details:

```text
Repository name: GetMyRoom
Repository owner/organization: Spiderotech
Repository URL: git@github.com:Spiderotech/GetMyRoom.git
Remote name: origin
Remote fetch URL: git@github.com:Spiderotech/GetMyRoom.git
Remote push URL: git@github.com:Spiderotech/GetMyRoom.git
Main branch: main
```

Useful git commands:

```bash
git status
git remote -v
git pull origin main
git push origin main
```

Recommended development branch flow:

```bash
git checkout main
git pull origin main
git checkout -b feature/<feature-name>
```

Note: the git repository stores the project source code. It does not mean the project is hosted. Frontend hosting, backend hosting, S3, database, DNS, and production credentials still need to be created/configured separately.

## Current Hosting Status

The project is currently not hosted.

| Resource | Status |
| --- | --- |
| Frontend hosting | Not created |
| Backend hosting | Not created |
| Production MongoDB | Must be configured |
| S3 bucket | Not created for this environment |
| AWS/IAM credentials | Not created for this environment |
| Email sender credentials | Must be configured securely |
| Domain/DNS | Not connected |
| SSL certificate | Not configured |

Although frontend constants currently point to `https://getmyroom.co.uk`, the project documentation treats hosting as pending because the current environment is not deployed and no active deployment credentials were provided.

## Technology Stack

Backend:

- Node.js
- Express
- MongoDB
- Mongoose
- JSON Web Tokens
- bcrypt
- Nodemailer
- AWS SDK and S3 pre-signed URLs
- Morgan
- CORS
- dotenv

Frontend:

- React 18
- TypeScript
- Vite
- Tailwind CSS
- Redux Toolkit
- Redux Persist
- React Router
- Axios
- Formik and Yup
- Headless UI
- Heroicons
- React Hot Toast
- Google OAuth package

## Application Structure

```text
GetMyRoom-new/
├── BACKEND/
│   ├── app.js
│   ├── package.json
│   └── src/
│       ├── adapters/
│       ├── application/
│       ├── config/
│       ├── entities/
│       └── framework/
├── FRONTEND/
│   ├── index.html
│   ├── package.json
│   ├── public/
│   ├── src/
│   └── dist/
├── docs/
└── README.md
```

## Backend Summary

The backend starts from `BACKEND/app.js`.

Startup flow:

1. Create an Express app.
2. Create an HTTP server.
3. Apply Express middleware from `src/framework/webserver/express.js`.
4. Connect to MongoDB using `src/framework/database/connection.js`.
5. Register API routes from `src/framework/webserver/routes/index.js`.
6. Start the server using `src/framework/webserver/server.js`.

The backend code uses a layered structure:

- Controllers receive HTTP requests.
- Use cases contain application-specific behavior.
- Repository interfaces decouple use cases from MongoDB implementations.
- MongoDB repositories use Mongoose models.
- Services handle auth, OTP, email, and integrations.

## Frontend Summary

The frontend starts from `FRONTEND/src/main.tsx` and `FRONTEND/src/App.tsx`.

Route groups:

- Public/user routes are loaded from `FRONTEND/src/Routes/UserRoutes.tsx`.
- Admin routes are loaded from `FRONTEND/src/Routes/AdminRoutes.tsx`.

Main user pages:

- Home
- Listing page
- Property detail page
- Add property form
- Saved properties
- My listings
- Profile
- Email contact
- Privacy
- Terms

Main admin pages:

- Login
- Dashboard
- Users
- Listed properties
- Unlisted properties
- Property details

## API Route Groups

Backend route groups:

- `/api/v1/user`
- `/api/v1/property`
- `/api/v1/admin`
- `/api/v1/service`

See [API Documentation](API_DOCUMENTATION.md) for endpoint details.

## Data Models

Main MongoDB models:

- `Userdata`
- `Properties`
- `admindatas`

See [Database Documentation](DATABASE.md) for model details.

## Environment and Credentials

Development and production should use different environment values. No production credentials should be committed to git.

Required credential groups:

- MongoDB URI
- JWT access token secret
- JWT refresh token secret
- S3 access key
- S3 secret key
- S3 bucket name
- Email sender account
- Email app password or SMTP credentials
- Frontend API base URL

Current risk: `BACKEND/src/config/config.js` contains hard-coded MongoDB and email values. Move these values to `.env`, rotate exposed credentials, and update the config file to read from environment variables only.

## Related Documents

- [Architecture](ARCHITECTURE.md)
- [Folder Structure](FOLDER_STRUCTURE.md)
- [Frontend Functionality](FRONTEND_FUNCTIONALITY.md)
- [API Documentation](API_DOCUMENTATION.md)
- [Environment Setup](ENVIRONMENT.md)
- [Database Documentation](DATABASE.md)
- [Development Guide](DEVELOPMENT.md)
- [Hosting Documentation](HOSTING_DOCUMENTATION.md)
