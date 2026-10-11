# Modern MERN Real Estate Marketplace

A full-stack, modern Real Estate Marketplace web application built with the **MERN Stack** (MongoDB, Express.js, React.js, Node.js), **Tailwind CSS**, **Redux Toolkit**, and **Firebase**.

Based on the tutorial: *[Build a Modern Real Estate Marketplace with react MERN (jwt, redux toolkit)](https://youtu.be/VAaUy_Moivw)* by Sahand Ghavidel.

---

## 🚀 Features

- **Authentication & Authorization**:
  - Email & Password sign-up and sign-in with salted password hashing (`bcryptjs`).
  - Google OAuth single sign-on integration (`Firebase` & backend user creation).
  - Secure JSON Web Token (`JWT`) authentication stored in HTTP-Only cookies.
  - Route guards (`PrivateRoute`) for authenticated-only sections.
- **State Management**:
  - Global state managed with **Redux Toolkit**.
  - Local storage persistence using **Redux Persist**.
- **User Profile Management**:
  - Update username, email, password, and profile picture avatar.
  - Cloud file uploads with progress bar via Firebase Storage.
  - Account deletion and sign-out.
  - "My Listings" management hub (view, edit, and delete personal listings).
- **Listing Management**:
  - Create, view, update, and delete property listings with ownership validation.
  - Multi-image uploads (up to 6 images) with previews.
  - Options for Rent vs Sale, Furnished, Parking, and Discounted Special Offers.
- **Interactive Listings & Search**:
  - Modern Swiper carousel image gallery for listings.
  - Direct contact landlord email messaging feature (`mailto` integration).
  - Shareable link button with copy-to-clipboard notification.
  - Advanced search and filter panel (filter by keyword, type, offers, amenities, price, and sorting order) with pagination.

---

## 🛠️ Tech Stack

- **Frontend**:
  - React 18
  - Vite
  - Tailwind CSS & PostCSS
  - Redux Toolkit & Redux Persist
  - React Router DOM v6
  - Swiper.js
  - React Icons
  - Firebase Client SDK
- **Backend**:
  - Node.js (ES Modules)
  - Express.js
  - MongoDB & Mongoose
  - JSON Web Tokens (`jsonwebtoken`)
  - Cookie-Parser
  - Bcrypt.js
  - Dotenv

---

## 📁 Directory Structure

```
mern-estate/
├── api/
│   ├── controllers/
│   │   ├── auth.controller.js
│   │   ├── listing.controller.js
│   │   └── user.controller.js
│   ├── models/
│   │   ├── listing.model.js
│   │   └── user.model.js
│   ├── routes/
│   │   ├── auth.route.js
│   │   ├── listing.route.js
│   │   └── user.route.js
│   ├── utils/
│   │   ├── error.js
│   │   └── verifyUser.js
│   └── index.js
├── client/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Contact.jsx
│   │   │   ├── Header.jsx
│   │   │   ├── ListingItem.jsx
│   │   │   ├── OAuth.jsx
│   │   │   └── PrivateRoute.jsx
│   │   ├── pages/
│   │   │   ├── About.jsx
│   │   │   ├── CreateListing.jsx
│   │   │   ├── Home.jsx
│   │   │   ├── Listing.jsx
│   │   │   ├── Profile.jsx
│   │   │   ├── Search.jsx
│   │   │   ├── SignIn.jsx
│   │   │   ├── SignUp.jsx
│   │   │   └── UpdateListing.jsx
│   │   ├── redux/
│   │   │   ├── user/
│   │   │   │   └── userSlice.js
│   │   │   └── store.js
│   │   ├── App.jsx
│   │   ├── firebase.js
│   │   ├── index.css
│   │   └── main.jsx
│   ├── index.html
│   ├── package.json
│   ├── postcss.config.js
│   ├── tailwind.config.js
│   └── vite.config.js
├── package.json
├── .env.example
├── .gitignore
└── README.md
```

---

## ⚙️ Configuration & Setup

### 1. Environment Variables
Create a `.env` file in the root directory:
```env
MONGO=mongodb://127.0.0.1:27017/mern-estate
# Or MongoDB Atlas:
# MONGO=mongodb+srv://<username>:<password>@cluster0.mongodb.net/mern-estate?retryWrites=true&w=majority

JWT_SECRET=supersecretjwtkey_12345
PORT=3000
```

### 2. Firebase Configuration (Optional for Google OAuth & Cloud Image Uploads)
1. Go to the [Firebase Console](https://console.firebase.google.com/) and create a project.
2. Enable **Authentication** with the **Google** provider.
3. Enable **Cloud Storage** and configure the storage rules:
```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read;
      allow write: if
      request.resource.size < 2 * 1024 * 1024 &&
      request.resource.contentType.matches('image/.*')
    }
  }
}
```
4. Copy your web app config and paste your `apiKey` into `client/.env`:
```env
VITE_FIREBASE_API_KEY=your_firebase_api_key_here
```
Or update `client/src/firebase.js` with your Firebase credentials.

---

## 🏃 Running the Application

### Install Dependencies
From the root directory:
```bash
# Install backend dependencies
npm install

# Install frontend dependencies
npm install --prefix client
```

### Development Mode
In two separate terminals:

**Terminal 1 (Backend Server):**
```bash
npm run dev
# Starts Express server on http://localhost:3000
```

**Terminal 2 (Frontend Client):**
```bash
npm run dev --prefix client
# Starts Vite dev server on http://localhost:5173
```

Open `http://localhost:5173` in your browser. All API requests are proxied from Vite to `http://localhost:3000`.

### Production Build
To create a production build of the frontend and run the unified server:
```bash
npm run build
npm start
```
The Express server will serve the compiled React SPA from `client/dist`.
