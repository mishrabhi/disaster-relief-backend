# Disaster Relief Backend

A robust Node.js/Express server powering the Disaster Relief platform. This backend handles user authentication, manages missing person reports, found person reports, donations, and real-time communication using Socket.io.

**Live URL:** https://disaster-relief-backend-x5uo.onrender.com

## 🌟 Features

### Authentication
- **User Registration** - Create accounts with email and password
- **User Login** - Secure JWT-based authentication
- **OAuth Support** - Google and Facebook authentication via Passport.js
- **Role-Based Access Control** - Different permissions for users, volunteers, and admins
- **Password Hashing** - BCrypt encryption for secure password storage

### Missing Person Management
- **Create Reports** - Submit detailed missing person reports with photos and location data
- **View Reports** - Retrieve all missing person reports with filters and pagination
- **Update Reports** - Modify report details and status
- **Delete Reports** - Remove reports (for authorized users)
- **Mark as Found** - Update status when a missing person is located

### Found Person Management
- **Report Found Persons** - Submit reports of found persons
- **Match Reports** - Link found reports with missing person reports
- **Update Findings** - Track and update found person information
- **Notification System** - Alert relevant users when matches are found

### Donation System
- **Pledge Donations** - Accept monetary and supply donations
- **Track Donations** - Maintain donation history and records
- **Multiple Types** - Support money, food, and clothing donations
- **Real-time Feed** - Live updates on donations via Socket.io

### Real-time Communication
- **Socket.io Integration** - Real-time notifications and updates
- **Live Notifications** - Instant alerts for new reports and found persons
- **Broadcasting** - Send updates to all connected clients

### File Management
- **Image Upload** - Upload missing person photos and evidence images
- **Cloudinary Integration** - Cloud storage for images with optimization
- **Automatic Processing** - Images are processed and optimized on upload

## 🛠️ Installation & Setup

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn
- MongoDB database (local or cloud)
- Cloudinary account (for image storage)
- OAuth credentials (Google and Facebook apps)

### Environment Variables

Create a `.env` file in the project root:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Database
MONGODB_URI=mongodb://localhost:27017/disaster-relief
# Or use MongoDB Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/disaster-relief

# JWT
JWT_SECRET=your_jwt_secret_key_here

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# OAuth - Google
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_CALLBACK_URL=http://localhost:5000/api/auth/google/callback

# OAuth - Facebook
FACEBOOK_APP_ID=your_facebook_app_id
FACEBOOK_APP_SECRET=your_facebook_app_secret
FACEBOOK_CALLBACK_URL=http://localhost:5000/api/auth/facebook/callback

# Frontend URL
CLIENT_URL=http://localhost:5173
```

### Steps

1. **Clone the repository**
```bash
git clone <repository-url>
cd Disaster_relief_backend
```

2. **Install dependencies**
```bash
npm install
```

3. **Configure environment variables**
```bash
cp .env.example .env
# Edit .env with your configuration
```

4. **Start MongoDB**
```bash
# If using local MongoDB
mongod

# Or use MongoDB Atlas cloud service
```

5. **Run the server**
```bash
# Development (with auto-reload)
npm run dev

# Production
npm start
```

The server will be available at `http://localhost:5000`

## 📡 API Endpoints

### Authentication Routes (`/api/auth`)
```
POST   /register               - Register a new user
POST   /login                  - Login with email/password
GET    /me                     - Get current user profile
GET    /google                 - Initiate Google OAuth
GET    /google/callback        - Google OAuth callback
GET    /facebook               - Initiate Facebook OAuth
GET    /facebook/callback      - Facebook OAuth callback
```

### Missing Person Routes (`/api/missing`)
```
POST   /                       - Create a new missing person report
GET    /                       - Get all missing person reports
GET    /:id                    - Get a specific missing person report
PUT    /:id                    - Update a missing person report
DELETE /:id                    - Delete a missing person report
PUT    /:id/status             - Update report status (found/still missing)
```

### Found Person Routes (`/api/found`)
```
POST   /                       - Create a found person report
GET    /                       - Get all found person reports
GET    /:id                    - Get a specific found person report
PUT    /:id                    - Update a found person report
DELETE /:id                    - Delete a found person report
```

### Donation Routes (`/api/donations`)
```
POST   /                       - Create a new donation pledge
GET    /                       - Get all donations
GET    /:id                    - Get a specific donation
PUT    /:id                    - Update a donation
DELETE /:id                    - Delete a donation
```

### Upload Routes (`/api/upload`)
```
POST   /                       - Upload image to Cloudinary
```

## 💻 Technologies Used

### Framework & Server
- **Express.js** - Web application framework
- **Node.js** - JavaScript runtime
- **Socket.io** - Real-time communication

### Database
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB object modeling

### Authentication
- **JWT (JSON Web Tokens)** - Token-based authentication
- **Passport.js** - Authentication middleware
- **bcryptjs** - Password hashing

### File Storage
- **Cloudinary** - Cloud image storage
- **Multer** - Middleware for file uploads
- **Multer-Storage-Cloudinary** - Multer storage engine for Cloudinary

### Utilities
- **Joi** - Data validation
- **dotenv** - Environment variable management
- **CORS** - Cross-Origin Resource Sharing
- **Express Async Handler** - Error handling for async functions

## 🔐 Security Features

- **JWT Token Authentication** - Secure API endpoint access
- **Password Hashing** - BCrypt for password encryption
- **CORS Protection** - Configured cross-origin access
- **Environment Variables** - Sensitive data protection
- **Input Validation** - Joi schema validation for all requests
- **OAuth Support** - Third-party secure authentication
- **Error Handling** - Centralized error management

## 🚀 Deployment

### Render.com (Current Hosting)
```bash
# The backend is deployed on Render.com
# Live URL: https://disaster-relief-backend-x5uo.onrender.com
```

### Environment-Specific Configuration
- **Development** - Local MongoDB, hot-reload with nodemon
- **Production** - MongoDB Atlas, optimized builds, CORS restricted to frontend domain

## 📋 Middleware

- **Authentication (`auth.js`)** - Verifies JWT tokens on protected routes
- **Error Handler (`errorHandler.js`)** - Centralized error handling
- **Upload (`upload.js`)** - Configures file upload to Cloudinary
- **CORS** - Enables cross-origin requests from frontend
