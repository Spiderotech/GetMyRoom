# Database Documentation

## Database

The backend uses MongoDB through Mongoose.

Connection file:

```text
BACKEND/src/framework/database/connection.js
```

Current model folder:

```text
BACKEND/src/framework/database/mongodb/models/
```

## Collections and Models

### Userdata

Model file:

```text
BACKEND/src/framework/database/mongodb/models/UserModel.js
```

Fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `name` | String | User name |
| `email` | String | User email |
| `password` | String | Hashed password for normal login |
| `image` | String | User profile image |
| `isBlock` | Boolean | User block status |
| `savedlist` | ObjectId array | Saved property references |
| `otp.value` | String | OTP value |
| `otp.expiresAt` | Date | OTP expiry |

### Properties

Model file:

```text
BACKEND/src/framework/database/mongodb/models/PropertyModel.js
```

Fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `userId` | ObjectId | Property owner/user reference |
| `title` | String | Property title |
| `type` | String | Property type |
| `location.locationName` | String | Human-readable location |
| `location.coordinates.lat` | Number | Latitude |
| `location.coordinates.lng` | Number | Longitude |
| `bathrooms` | Number | Bathroom count |
| `bedrooms` | Number | Bedroom count |
| `features.interiorDetails` | String array | Interior features |
| `features.otherFeatures` | String array | Other features |
| `features.outdoorDetails` | String array | Outdoor features |
| `features.utilities` | String array | Utility features |
| `image` | String array | Property image URLs |
| `description` | String | Property description |
| `price` | Number | Property price |
| `date` | String | Listing date |
| `approve` | Boolean | Admin approval/listing status |
| `floorplans` | String | Floorplan URL |
| `sellertype` | String | Seller type |

### admindatas

Model file:

```text
BACKEND/src/framework/database/mongodb/models/AdminModels.js
```

Fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `email` | String | Admin login email |
| `password` | String | Admin hashed password |

## Development Database

Recommended local database:

```env
MONGO_URI=mongodb://localhost:27017/getmyroom
```

If using MongoDB Atlas for development, create a separate development database:

```env
MONGO_URI=mongodb+srv://<dev-user>:<dev-password>@<cluster>/getmyroom_dev
```

## Production Database

Recommended production database:

```env
MONGO_URI=mongodb+srv://<prod-user>:<prod-password>@<cluster>/getmyroom_prod
```

Production recommendations:

- Use a dedicated database user with least privilege.
- Restrict network access to backend hosting IPs when possible.
- Enable backups.
- Enable monitoring.
- Use separate databases for dev/staging/prod.
- Rotate credentials after any accidental commit.

## Recommended Indexes

Add indexes as the data grows:

```js
Userdata: email unique index
Properties: userId index
Properties: approve index
Properties: type index
Properties: location.locationName index
```

Potential geospatial improvement:

```js
Properties: location.coordinates as 2dsphere
```

This requires changing the coordinate schema to GeoJSON format.
