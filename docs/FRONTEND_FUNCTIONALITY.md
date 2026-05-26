# Frontend Functionality

## Overview

The frontend is a React + TypeScript application built with Vite. It contains two main experiences:

- Public/user website for browsing, listing, saving, and contacting property owners.
- Admin dashboard for managing users and approving property listings.

Frontend root files:

```text
FRONTEND/src/main.tsx
FRONTEND/src/App.tsx
```

Route files:

```text
FRONTEND/src/Routes/UserRoutes.tsx
FRONTEND/src/Routes/AdminRoutes.tsx
```

## Frontend Route Map

### User Routes

| Route | Screen | Main Purpose |
| --- | --- | --- |
| `/` | Home page | Landing/search page for users |
| `/profile` | Profile page | View and update user profile/password |
| `/save` | Saved list page | View saved properties |
| `/mylist` | My listings page | View properties listed by the logged-in user |
| `/listdata` | Listing page | View filtered property listings |
| `/details` | Property detail page | View full details for one property |
| `/email` | Email contact page | Send property inquiry to owner |
| `/form` | Add your home page | Multi-step property listing form |
| `/privacy` | Privacy page | Privacy policy content |
| `/terms` | Terms page | Terms and conditions content |
| `*` | Not found page | Fallback screen |

### Admin Routes

| Route | Screen | Main Purpose |
| --- | --- | --- |
| `/admin` | Admin login | Admin authentication |
| `/admin/dashboard` | Dashboard | Entry page with links to admin sections |
| `/admin/user` | User list | View registered users |
| `/admin/listed` | Listed properties | View approved/listed properties |
| `/admin/unlisted` | Unlisted properties | View pending/unapproved properties |
| `/admin/details` | Property detail | Review unlisted property details |
| `/admin/listdetails` | Listed property detail | View listed property details |

## User Website Screens

### Home Page

Files:

```text
FRONTEND/src/Pages/Homepage.tsx
FRONTEND/src/Components/Home_Search.tsx
FRONTEND/src/Components/Header.tsx
FRONTEND/src/Components/Footer.tsx
```

Functionality:

- Shows the public home experience.
- Allows users to search/filter property listings by location and property type.
- Navigates to `/listdata?location=<location>&type=<type>` after search.
- Header gives access to profile, saved list, my listings, and add-property flow.
- If a user tries to access protected actions without login, login modal is opened.

### Listing Page

Files:

```text
FRONTEND/src/Pages/Listingpage.tsx
FRONTEND/src/Components/Listview.tsx
FRONTEND/src/Components/Mapview.tsx
FRONTEND/src/Components/Listcard.tsx
FRONTEND/src/Components/Filterbar.tsx
FRONTEND/src/Components/Filtnavbar.tsx
```

Functionality:

- Reads `location` and `type` from query parameters.
- Calls property API:

```text
GET /api/v1/property/getallproperty?location=<location>&type=<type>
```

- Displays properties in list/card view.
- Includes map-based listing view through `Mapview.tsx`.
- Property cards navigate to `/details?Id=<propertyId>`.
- Logged-in users can save a property from listing cards.

### Property Detail Page

Files:

```text
FRONTEND/src/Pages/Detaildatapage.tsx
FRONTEND/src/Components/Single_propertyDetails.tsx
```

Functionality:

- Reads property ID from query parameter.
- Calls property API:

```text
GET /api/v1/property/getsingleproperty?id=<propertyId>
```

- Shows property images, title, location, price, description, features, floor plan, and owner-related actions.
- Allows logged-in users to save the property.
- Navigates to inquiry screen using:

```text
/email?Id=<propertyId>
```

### Email Contact Page

Files:

```text
FRONTEND/src/Pages/Emailcontactpage.tsx
FRONTEND/src/Components/Emailcontact.tsx
```

Functionality:

- Loads property information for the selected property.
- Provides form fields for inquiry details.
- Sends inquiry through service API:

```text
POST /api/v1/service/nodemailer
```

- Redirects back to the property detail page after successful flow.

### Add Your Home Page

Files:

```text
FRONTEND/src/Pages/Addyourhomepage.tsx
FRONTEND/src/Components/Mutistepform.tsx
FRONTEND/src/Components/AddyourHome/
```

Step components:

```text
SellerType.tsx
Type.tsx
Location.tsx
Rooms.tsx
Price.tsx
Features.tsx
Description.tsx
Images.tsx
Videos.tsx
Floorplans.tsx
Hometitle.tsx
Stepdetails.tsx
Progressbar.tsx
```

Functionality:

- Multi-step form for property listing.
- Collects seller type, property type, location, rooms, price, features, description, images, videos/floorplans, and title.
- Uses service API to request S3 pre-signed upload URLs:

```text
GET /api/v1/service/s3service
```

- Submits final listing to property API:

```text
POST /api/v1/property/addnewproperty
```

- Redirects to `/mylist` after successful submission.

Important note:

- The backend controller currently expects `tilte` instead of `title`. Frontend and backend should be refactored together before changing this field.

### My Listings Page

Files:

```text
FRONTEND/src/Pages/Mylistpage.tsx
FRONTEND/src/Components/Mylist.tsx
FRONTEND/src/Components/Mylistcard.tsx
```

Functionality:

- Loads properties created by the logged-in user.
- Calls property API:

```text
GET /api/v1/property/getuserproperty?id=<userId>
```

- Displays listed properties.
- Allows removing a listed property:

```text
POST /api/v1/property/removeproperty
```

- Provides navigation back to add a new listing.

### Saved List Page

Files:

```text
FRONTEND/src/Pages/Savedpage.tsx
FRONTEND/src/Components/Savedlist.tsx
FRONTEND/src/Components/Savedcard.tsx
```

Functionality:

- Loads saved properties for the logged-in user.
- Calls user API:

```text
GET /api/v1/user/getsavedjobs?id=<userId>
```

- Allows removing a saved property:

```text
POST /api/v1/user/removeproperty
```

- Property card click opens `/details?Id=<propertyId>`.

Recommended naming improvement:

- Rename `/getsavedjobs` to `/getsavedproperties` in a coordinated frontend/backend change.

### Profile Page

Files:

```text
FRONTEND/src/Pages/Profilepage.tsx
FRONTEND/src/Components/Profile.tsx
FRONTEND/src/Components/Modals/Editprofile.tsx
```

Functionality:

- Loads user profile:

```text
GET /api/v1/user/getprofile?id=<userId>
```

- Updates name, email, and image:

```text
POST /api/v1/user/updateuserdata
```

- Updates password:

```text
POST /api/v1/user/updatepassword
```

- Uses S3 service for profile image upload when needed.
- Updates Redux user state and local storage tokens after profile update responses.

### Privacy and Terms Pages

Files:

```text
FRONTEND/src/Pages/Privacy.tsx
FRONTEND/src/Components/Privacypolicy.tsx
FRONTEND/src/Pages/Termsandcondtionpage.tsx
FRONTEND/src/Components/Termsandcondition.tsx
```

Functionality:

- Static legal/policy pages for the website.
- Header/footer navigation can link users to these pages.

## Authentication and Modals

Files:

```text
FRONTEND/src/Components/Modals/LoginModal.tsx
FRONTEND/src/Components/Modals/Login.tsx
FRONTEND/src/Components/Modals/Loginform.tsx
FRONTEND/src/Components/Modals/Logincomponent.tsx
FRONTEND/src/Components/Modals/Registerform.tsx
FRONTEND/src/Components/Modals/Registercomponent.tsx
FRONTEND/src/Components/Modals/Terms.tsx
```

User registration flow:

```text
POST /api/v1/user/register
POST /api/v1/user/verifyotp
POST /api/v1/user/adduserdata
```

User login flow:

```text
POST /api/v1/user/login
```

OTP login/password flows:

```text
POST /api/v1/user/verifyotplogin
POST /api/v1/user/checkemail
POST /api/v1/user/updatepassword
```

Google auth flows:

```text
POST /api/v1/user/googlesignup
POST /api/v1/user/googlelogin
```

Terms modal:

- Uses `localStorage` key `isModalDisplayed`.
- Displays terms-related modal logic once per configured session/window behavior.

## Admin Screens

### Admin Login

Files:

```text
FRONTEND/src/Components/admin/Pages/Loginpage.tsx
FRONTEND/src/Components/admin/Components/Login.tsx
```

Functionality:

- Collects admin email and password.
- Calls:

```text
POST /api/v1/admin/login
```

- Stores admin tokens in local storage.
- Stores admin state in Redux.
- Navigates to `/admin/dashboard` after successful login.

### Admin Dashboard

Files:

```text
FRONTEND/src/Components/admin/Pages/dashboard.tsx
FRONTEND/src/Components/admin/Components/Dashboard.tsx
```

Functionality:

- Provides admin navigation cards/links.
- Links to users, listed properties, and unlisted properties.

### Admin User List

Files:

```text
FRONTEND/src/Components/admin/Pages/Userlistpage.tsx
FRONTEND/src/Components/admin/Components/Usercard.tsx
```

Functionality:

- Loads users from:

```text
GET /api/v1/admin/getuserdetails
```

- Displays registered users in admin view.

### Admin Listed Properties

Files:

```text
FRONTEND/src/Components/admin/Pages/Listedpropertypage.tsx
FRONTEND/src/Components/admin/Components/Propertycard2.tsx
FRONTEND/src/Components/admin/Pages/listedpropertydetailspage.tsx
FRONTEND/src/Components/admin/Components/Propertydetaillisted.tsx
```

Functionality:

- Loads approved/listed properties:

```text
GET /api/v1/admin/getuserlistedproperty
```

- Shows property cards and listed property detail page.
- Allows admin to remove a listed property through property API:

```text
POST /api/v1/property/removeproperty
```

### Admin Unlisted Properties

Files:

```text
FRONTEND/src/Components/admin/Pages/Unlistedpropertypage.tsx
FRONTEND/src/Components/admin/Components/Propertycard.tsx
FRONTEND/src/Components/admin/Pages/Propertydetailpage.tsx
FRONTEND/src/Components/admin/Components/Propertydetails.tsx
```

Functionality:

- Loads pending/unapproved properties:

```text
GET /api/v1/admin/getuserunlistedproperty
```

- Opens details through `/admin/details?Id=<propertyId>`.
- Approves/verifies property:

```text
POST /api/v1/admin/verify
```

- Navigates to `/admin/listed` after successful approval.

## State Management

Files:

```text
FRONTEND/src/redux/store.ts
FRONTEND/src/redux/reducer/userSlice.ts
FRONTEND/src/redux/reducer/AdminSlice.ts
```

Redux slices:

| Slice | Purpose |
| --- | --- |
| `user` | Stores current user ID, name, email, image, and access token |
| `admin` | Stores current admin ID, email, and access token |

Persistence:

- Uses `redux-persist`.
- Stores Redux state in browser local storage.

Token storage:

```text
access_token_user
refresh_token_user
access_token_admin
refresh_token_admin
```

Known issue:

- `userSlice.ts` removes `refresh_token-user`, but other code stores `refresh_token_user`. The key name should be made consistent.

## API Client Setup

Axios clients:

```text
FRONTEND/src/Components/Utils/user/axios.ts
FRONTEND/src/Components/Utils/property/axios.ts
FRONTEND/src/Components/Utils/Ssrvice/axios.ts
FRONTEND/src/Components/admin/Utils/axios.ts
```

Current base URL files:

```text
FRONTEND/src/Components/Utils/user/constant.ts
FRONTEND/src/Components/Utils/property/constant.ts
FRONTEND/src/Components/admin/Utils/constant.ts
```

Current configured API domain:

```text
https://getmyroom.co.uk/api/v1
```

Recommended improvement:

- Move API URLs to Vite environment variables using `VITE_API_BASE_URL`.
- Use separate local, staging, and production values.

## Frontend Working Flow Summary

Typical user flow:

```text
Home
  -> Search listings
  -> Listing page
  -> Property detail
  -> Save property or contact owner
```

Typical property listing flow:

```text
Login/Register
  -> Add Your Home
  -> Complete multi-step form
  -> Upload images/floorplans through S3 signed URL
  -> Submit property
  -> My Listings
  -> Wait for admin approval
```

Typical admin flow:

```text
Admin login
  -> Dashboard
  -> Unlisted properties
  -> Property details
  -> Verify property
  -> Listed properties
```

## Frontend Improvement Checklist

- [ ] Move hard-coded API URLs to `.env`.
- [ ] Add route guards for logged-in user pages.
- [ ] Add route guards for admin pages.
- [ ] Normalize token local storage key names.
- [ ] Add loading and error states to all API screens.
- [ ] Add form validation consistency across auth, profile, and property forms.
- [ ] Fix `tilte` field spelling with backend coordination.
- [ ] Rename service folder `Ssrvice` to `Service` with import updates.
- [ ] Add automated frontend tests for auth, listings, property details, and admin approval.
