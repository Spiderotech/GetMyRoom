# Environment Setup

## Current Environment Status

The project does not currently include `.env` files. The backend uses `dotenv`, but some values are hard-coded in `BACKEND/src/config/config.js`.

Before development or production usage:

- Move hard-coded database URI to environment variables.
- Move hard-coded email username/password to environment variables.
- Rotate any exposed credentials.
- Add `.env.example` files with placeholder values only.
- Configure separate values for development and production.

## Backend Environment

Create:

```text
BACKEND/.env
```

Development example:

```env
PORT=3000
MONGO_URI=mongodb://localhost:27017/getmyroom
ACESS_TOKEN_SCERET=dev_access_token_secret
REFRESH_TOKEN_SECRET=dev_refresh_token_secret
AWS_REGION=ap-south-1
S3_BUCKET_NAME=getmyroom-dev-assets
S3_ACESS_KEY=replace_after_s3_is_created
S3_SECRET_KEY=replace_after_s3_is_created
EMAIL=dev_sender@example.com
PASSWORD=dev_email_app_password
```

Production example:

```env
PORT=3000
MONGO_URI=mongodb+srv://<username>:<password>@<cluster>/<database>
ACESS_TOKEN_SCERET=strong_production_access_secret
REFRESH_TOKEN_SECRET=strong_production_refresh_secret
AWS_REGION=ap-south-1
S3_BUCKET_NAME=getmyroom-prod-assets
S3_ACESS_KEY=replace_after_prod_s3_is_created
S3_SECRET_KEY=replace_after_prod_s3_is_created
EMAIL=production_sender@example.com
PASSWORD=production_email_or_smtp_password
```

## Frontend Environment

The frontend currently uses hard-coded API URLs in:

```text
FRONTEND/src/Components/Utils/user/constant.ts
FRONTEND/src/Components/Utils/property/constant.ts
FRONTEND/src/Components/admin/Utils/constant.ts
FRONTEND/src/Components/Utils/Ssrvice/axios.ts
```

Recommended future setup:

```text
FRONTEND/.env
```

Development:

```env
VITE_API_BASE_URL=http://localhost:3000/api/v1
```

Production:

```env
VITE_API_BASE_URL=https://api.getmyroom.co.uk/api/v1
```

Recommended frontend constants after refactor:

```ts
const apiBaseUrl = import.meta.env.VITE_API_BASE_URL;

export const userBaseUrl = `${apiBaseUrl}/user`;
export const propertyBaseUrl = `${apiBaseUrl}/property`;
export const adminBaseUrl = `${apiBaseUrl}/admin`;
export const serviceBaseUrl = `${apiBaseUrl}/service`;
```

## Secret Handling Rules

- Do not commit real `.env` files.
- Do not commit database passwords, email passwords, JWT secrets, or cloud keys.
- Use hosting provider environment variables for production.
- Use different credentials for development and production.
- Rotate credentials if they were committed or shared.
- Prefer IAM roles over static AWS keys when the hosting platform supports them.

## Suggested `.gitignore` Entries

```gitignore
node_modules/
dist/
.env
.env.local
.env.development
.env.production
.DS_Store
npm-debug.log*
```
