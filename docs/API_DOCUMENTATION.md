# API Documentation

## Base URL

Local development:

```text
http://localhost:3000/api/v1
```

Production after hosting:

```text
https://api.getmyroom.co.uk/api/v1
```

The backend route groups are registered in `BACKEND/src/framework/webserver/routes/index.js`.

## User APIs

Base path:

```text
/api/v1/user
```

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `POST` | `/register` | Start user registration and OTP flow |
| `POST` | `/verifyotp` | Verify registration OTP |
| `POST` | `/login` | User login |
| `POST` | `/adduserdata` | Add user profile data after OTP verification |
| `GET` | `/getprofile?id=<userId>` | Get user profile |
| `POST` | `/verifyotplogin` | Verify OTP during login flow |
| `POST` | `/save` | Save a property to user's saved list |
| `GET` | `/getsavedjobs?id=<userId>` | Get saved properties |
| `POST` | `/googlesignup` | Create user with Google account data |
| `POST` | `/googlelogin` | Login with Google account data |
| `POST` | `/removeproperty` | Remove a property from saved list |
| `POST` | `/updateuserdata` | Update user profile data |
| `POST` | `/checkemail` | Verify/check email for password update |
| `POST` | `/updatepassword` | Update password |

Example login body:

```json
{
  "email": "user@example.com",
  "password": "password"
}
```

Example save property body:

```json
{
  "UserId": "user_id",
  "postId": "property_id"
}
```

## Property APIs

Base path:

```text
/api/v1/property
```

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `POST` | `/addnewproperty` | Create a new property listing |
| `GET` | `/getuserproperty?id=<userId>` | Get properties created by one user |
| `GET` | `/getallproperty?location=<location>&type=<type>` | Get approved/listable properties, optionally filtered |
| `GET` | `/getsingleproperty?id=<propertyId>` | Get one property |
| `POST` | `/removeproperty` | Remove a listed property |

Example add property body:

```json
{
  "userId": "user_id",
  "tilte": "2 BHK Apartment",
  "type": "Apartment",
  "location": {
    "locationName": "London",
    "coordinates": {
      "lat": 51.5072,
      "lng": -0.1276
    }
  },
  "bathrooms": 2,
  "bedrooms": 2,
  "features": {
    "interiorDetails": [],
    "otherFeatures": [],
    "outdoorDetails": [],
    "utilities": []
  },
  "image": [],
  "description": "Property description",
  "price": 1200,
  "floorplans": "floorplan-url",
  "seller": "owner"
}
```

Note: the current controller expects `tilte`, not `title`. This should be corrected carefully in both frontend and backend when refactoring.

## Admin APIs

Base path:

```text
/api/v1/admin
```

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `POST` | `/login` | Admin login |
| `GET` | `/getuserdetails` | Get users |
| `GET` | `/getuserlistedproperty` | Get listed/approved properties |
| `GET` | `/getuserunlistedproperty` | Get unlisted/unapproved properties |
| `POST` | `/verify` | Approve/verify a property |

Example admin login body:

```json
{
  "email": "admin@example.com",
  "password": "password"
}
```

Example verify property body:

```json
{
  "postId": "property_id"
}
```

## Service APIs

Base path:

```text
/api/v1/service
```

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `GET` | `/s3service` | Generate a pre-signed S3 upload URL |
| `POST` | `/nodemailer` | Send property inquiry email |

Example email body depends on `commonservicecontroller.js`, but the email use case expects values similar to:

```json
{
  "fullname": "User Name",
  "email": "user@example.com",
  "message": "I am interested in this property.",
  "useremail": "owner@example.com",
  "propertyname": "2 BHK Apartment",
  "location": "London",
  "name": "Owner Name"
}
```

## Recommended API Improvements

- Add request validation for all POST bodies.
- Add consistent success/error response shapes.
- Add auth middleware to protected user/admin routes.
- Add pagination for property and user listing APIs.
- Add a health check endpoint.
- Rename `/getsavedjobs` to a property-specific name, for example `/getsavedproperties`.
- Fix the `tilte` field spelling after coordinating frontend and backend changes.
