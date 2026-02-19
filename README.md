# Wanderlust

**A Full-Stack Travel Accommodation Platform**

Wanderlust is a feature-rich web application inspired by Airbnb, built with Node.js and Express.js. It allows users to explore, create, and review travel accommodations worldwide, complete with interactive maps, image uploads, and secure user authentication.

[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue?logo=github)](https://github.com/Rajendra0309/Wanderlust)
[![Node.js](https://img.shields.io/badge/Node.js-v24.0.2-green?logo=node.js)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-green?logo=mongodb)](https://www.mongodb.com/)

---

## Features

- **Listing Management**: Create, read, update, and delete travel accommodation listings
- **Review System**: Users can leave reviews and ratings for properties
- **User Authentication**: Secure login/signup using Passport.js with local strategy
- **Interactive Maps**: Integration with Mapbox API for location visualization and geocoding
- **Image Upload**: Cloud-based image storage using Cloudinary
- **Authorization**: Owner-based permissions for editing and deleting listings
- **Data Validation**: Server-side validation using Joi schema
- **Flash Messages**: Real-time user feedback for actions
- **Responsive Design**: Mobile-friendly UI with Bootstrap/CSS
- **Dynamic Templating**: EJS templates with layouts using ejs-mate
- **Session Management**: Persistent sessions stored in MongoDB

---

## Tech Stack

### Backend
- **Node.js** - JavaScript runtime
- **Express.js** - Web application framework
- **MongoDB Atlas** - Cloud database
- **Mongoose** - MongoDB object modeling

### Authentication & Security
- **Passport.js** - Authentication middleware
- **Passport-Local** - Username and password authentication
- **Passport-Local-Mongoose** - Mongoose plugin for user authentication
- **Express-Session** - Session middleware
- **Connect-Mongo** - MongoDB session store

### Cloud Services
- **Cloudinary** - Image storage and management
- **Mapbox SDK** - Geocoding and mapping services

### Validation & Error Handling
- **Joi** - Schema validation
- **Custom Error Handler** - Centralized error management

### Frontend
- **EJS** - Templating engine
- **EJS-Mate** - Layout support for EJS
- **CSS** - Custom styling
- **JavaScript** - Client-side interactivity

### Additional Tools
- **Multer** - File upload handling
- **Method-Override** - HTTP method override
- **Connect-Flash** - Flash messages
- **Dotenv** - Environment variable management

---

## Project Structure

```
Wanderlust/
├── app.js                  # Main application entry point
├── package.json            # Dependencies and scripts
├── cloudConfig.js          # Cloudinary configuration
├── middleware.js           # Custom middleware (auth, validation)
├── schema.js              # Joi validation schemas
├── controllers/
│   ├── listings.js        # Listing business logic
│   ├── reviews.js         # Review business logic
│   └── users.js           # User authentication logic
├── models/
│   ├── listing.js         # Listing schema
│   ├── review.js          # Review schema
│   └── user.js            # User schema
├── routes/
│   ├── listing.js         # Listing routes
│   ├── review.js          # Review routes
│   └── user.js            # User routes
├── views/
│   ├── layouts/           # EJS layouts
│   ├── listings/          # Listing views
│   ├── users/             # Authentication views
│   └── includes/          # Reusable components (navbar, footer, flash)
├── public/
│   ├── css/               # Stylesheets
│   └── js/                # Client-side JavaScript (map, scripts)
├── utils/
│   ├── ExpressError.js    # Custom error class
│   └── wrapAsync.js       # Async error wrapper
└── init/
    ├── data.js            # Sample data
    └── index.js           # Database initialization script
```

---

## Getting Started

### Prerequisites

- Node.js (v24.0.2 or higher)
- MongoDB Atlas account
- Cloudinary account
- Mapbox account

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Rajendra0309/Wanderlust.git
   cd Wanderlust
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the root directory with the following variables:
   ```env
   ATLASDB_URL=your_mongodb_atlas_connection_string
   SECRET=your_session_secret_key
   
   # Cloudinary Configuration
   CLOUD_NAME=your_cloudinary_cloud_name
   CLOUD_API_KEY=your_cloudinary_api_key
   CLOUD_API_SECRET=your_cloudinary_api_secret
   
   # Mapbox Configuration
   MAP_TOKEN=your_mapbox_access_token
   
   # Environment
   NODE_ENV=development
   ```

4. **Initialize the database (optional)**
   
   To populate the database with sample data:
   ```bash
   node init/index.js
   ```

5. **Start the development server**
   ```bash
   npm start
   ```
   or with nodemon for auto-restart:
   ```bash
   npx nodemon app.js
   ```

6. **Access the application**
   
   Open your browser and navigate to:
   ```
   http://localhost:3000
   ```

---

## Usage

### For Users
1. **Sign Up/Login**: Create an account or log in to access full features
2. **Browse Listings**: View all available accommodations on the homepage
3. **View Details**: Click on any listing to see detailed information, reviews, and location map
4. **Add Review**: Leave ratings and reviews for properties you've visited
5. **Create Listing**: Share your own property by creating a new listing with images and location

### For Listing Owners
1. **Manage Listings**: Edit or delete your own property listings
2. **Upload Images**: Add professional photos using the integrated Cloudinary upload
3. **Set Location**: Automatic geocoding converts addresses to map coordinates

---

## Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `ATLASDB_URL` | MongoDB Atlas connection string | `mongodb+srv://<username>:<password>@cluster.mongodb.net/wanderlust` |
| `SECRET` | Session secret key for encryption | `your-secret-key-here` |
| `CLOUD_NAME` | Cloudinary cloud name | `your-cloud-name` |
| `CLOUD_API_KEY` | Cloudinary API key | `your-api-key` |
| `CLOUD_API_SECRET` | Cloudinary API secret | `your-api-secret` |
| `MAP_TOKEN` | Mapbox public access token | `pk.eyJ1IjoiZXhhbXBsZSIsImEiOiJja...` |
| `NODE_ENV` | Environment mode | `development` or `production` |

---

## API Routes

### Listings
- `GET /listings` - View all listings
- `GET /listings/new` - Show create listing form (auth required)
- `POST /listings` - Create new listing (auth required)
- `GET /listings/:id` - View single listing details
- `GET /listings/:id/edit` - Show edit form (owner only)
- `PUT /listings/:id` - Update listing (owner only)
- `DELETE /listings/:id` - Delete listing (owner only)

### Reviews
- `POST /listings/:id/reviews` - Add review to listing (auth required)
- `DELETE /listings/:id/reviews/:reviewId` - Delete review (author only)

### Users
- `GET /signup` - Show signup form
- `POST /signup` - Register new user
- `GET /login` - Show login form
- `POST /login` - Authenticate user
- `GET /logout` - Logout user

---

## Security Features

- **Password Hashing**: User passwords are hashed using passport-local-mongoose
- **Session Management**: Secure sessions with httpOnly cookies
- **CSRF Protection**: Session-based authentication
- **Input Validation**: Joi schema validation on all inputs
- **Authorization Checks**: Middleware ensures users can only modify their own content
- **Environment Variables**: Sensitive data stored securely in .env file

---

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## License

This project is open source and available under the [ISC License](LICENSE).

---

## Author

**Rajendra Guttedar**

- GitHub: [@Rajendra0309](https://github.com/Rajendra0309)
- LinkedIn: [Connect with me](https://www.linkedin.com/in/rajendra0309)

---

## Acknowledgments

- Inspired by Airbnb's user experience
- [Mapbox](https://www.mapbox.com/) for mapping services
- [Cloudinary](https://cloudinary.com/) for image management
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) for cloud database hosting
