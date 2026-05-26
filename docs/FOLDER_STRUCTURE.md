# Folder Structure

## Root

```text
GetMyRoom-new/
├── BACKEND/
├── FRONTEND/
├── docs/
└── README.md
```

Root responsibilities:

- `BACKEND/`: API server.
- `FRONTEND/`: React client.
- `docs/`: project, hosting, architecture, API, and setup documents.
- `README.md`: project entry documentation.

## Backend Folder Structure

```text
BACKEND/
├── app.js
├── package.json
├── package-lock.json
└── src/
    ├── adapters/
    │   └── controllers/
    │       ├── admin/
    │       ├── user/
    │       └── commonservicecontroller.js
    ├── application/
    │   ├── repositories/
    │   │   ├── admin/
    │   │   └── user/
    │   ├── services/
    │   │   ├── admin/
    │   │   └── user/
    │   └── useCase/
    │       ├── admin/
    │       ├── common/
    │       └── user/
    ├── config/
    │   └── config.js
    ├── entities/
    └── framework/
        ├── database/
        │   ├── connection.js
        │   └── mongodb/
        │       ├── models/
        │       └── repositories/
        ├── services/
        │   ├── admin/
        │   └── user/
        └── webserver/
            ├── express.js
            ├── routes/
            └── server.js
```

Important backend files:

| File | Purpose |
| --- | --- |
| `BACKEND/app.js` | Main backend entry point |
| `src/config/config.js` | Environment/config values |
| `src/framework/webserver/express.js` | Express middleware setup |
| `src/framework/webserver/server.js` | Server listener setup |
| `src/framework/webserver/routes/index.js` | API route registration |
| `src/framework/database/connection.js` | MongoDB connection |
| `src/framework/database/mongodb/models/UserModel.js` | User schema |
| `src/framework/database/mongodb/models/PropertyModel.js` | Property schema |
| `src/framework/database/mongodb/models/AdminModels.js` | Admin schema |

## Frontend Folder Structure

```text
FRONTEND/
├── index.html
├── package.json
├── package-lock.json
├── public/
├── src/
│   ├── App.tsx
│   ├── main.tsx
│   ├── index.css
│   ├── App.css
│   ├── Routes/
│   ├── Pages/
│   ├── Components/
│   │   ├── AddyourHome/
│   │   ├── Modals/
│   │   ├── Skeletons/
│   │   ├── Utils/
│   │   └── admin/
│   ├── assets/
│   └── redux/
├── dist/
├── tailwind.config.js
├── postcss.config.js
├── tsconfig.json
└── vite.config.ts
```

Important frontend files:

| File | Purpose |
| --- | --- |
| `src/main.tsx` | React app entry point |
| `src/App.tsx` | Root routes |
| `src/Routes/UserRoutes.tsx` | Public/user routes |
| `src/Routes/AdminRoutes.tsx` | Admin routes |
| `src/redux/store.ts` | Redux store |
| `src/redux/reducer/userSlice.ts` | User state |
| `src/redux/reducer/AdminSlice.ts` | Admin state |
| `src/Components/Utils/user/constant.ts` | User API base URL |
| `src/Components/Utils/property/constant.ts` | Property API base URL |
| `src/Components/admin/Utils/constant.ts` | Admin API base URL |

## Generated/Build Folders

`FRONTEND/dist/` contains built frontend assets. It can be regenerated with:

```bash
cd FRONTEND
npm run build
```

For source control, decide whether to commit `dist/`. Most Vite projects do not commit build output unless a specific deployment workflow requires it.
