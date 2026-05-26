# Architecture

## High-Level Architecture

```text
Browser
  |
  | React/Vite frontend
  v
Express REST API
  |
  | Mongoose repositories
  v
MongoDB

Express API also integrates with:
- S3 for pre-signed upload URLs
- SMTP/email provider for property inquiry emails
- JWT/bcrypt for authentication
```

## Backend Layers

The backend follows a layered structure:

```text
src/
├── adapters/controllers/
├── application/
│   ├── repositories/
│   ├── services/
│   └── useCase/
├── config/
├── entities/
└── framework/
    ├── database/
    ├── services/
    └── webserver/
```

Layer responsibilities:

| Layer | Responsibility |
| --- | --- |
| `framework/webserver` | Express setup, server startup, route registration |
| `adapters/controllers` | Converts HTTP requests into use case calls |
| `application/useCase` | Business actions such as register, login, add property, approve property |
| `application/repositories` | Repository interfaces |
| `framework/database/mongodb/repositories` | MongoDB repository implementations |
| `framework/database/mongodb/models` | Mongoose schemas/models |
| `framework/services` | Concrete auth and OTP services |
| `application/services` | Service interfaces |

## Frontend Architecture

The frontend is a Vite React app:

```text
src/
├── App.tsx
├── main.tsx
├── Routes/
├── Pages/
├── Components/
└── redux/
```

Key concepts:

- `App.tsx` defines root routing.
- `Routes/UserRoutes.tsx` defines user-facing routes.
- `Routes/AdminRoutes.tsx` defines admin routes.
- `Pages/` contains route-level user pages.
- `Components/` contains reusable UI and feature components.
- `Components/admin/` contains admin dashboard pages/components.
- `redux/` contains Redux store and slices.
- Axios clients are stored under `Components/Utils/` and `Components/admin/Utils/`.

## Request Flow Example

Adding a property:

```text
Frontend Add Your Home form
  -> POST /api/v1/property/addnewproperty
  -> propertycontroller.addproperty
  -> application/useCase/user/addproperty.js
  -> userpropertyrepositoryInt
  -> userpropertyrepositoryImp
  -> Property mongoose model
  -> MongoDB
```

## Authentication Flow

User registration:

```text
POST /api/v1/user/register
  -> create OTP / send OTP
POST /api/v1/user/verifyotp
  -> verify OTP
POST /api/v1/user/adduserdata
  -> create user with hashed password
```

User login:

```text
POST /api/v1/user/login
  -> validate password
  -> return auth response/token data
```

Admin login:

```text
POST /api/v1/admin/login
  -> validate admin credentials
  -> return admin auth response/token data
```

## Integration Points

S3 upload URL:

```text
GET /api/v1/service/s3service
```

Email inquiry:

```text
POST /api/v1/service/nodemailer
```

## Current Architecture Risks

- Secrets are hard-coded in backend config and must be moved to environment variables.
- Frontend API base URLs are hard-coded to a production domain.
- CORS currently allows all origins.
- There is no dedicated health check endpoint.
- Route-level authentication middleware is not clearly applied in route definitions.
- Tests are not currently present.
