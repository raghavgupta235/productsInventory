# Products Inventory API Server

A Node.js Express server for managing products inventory with MongoDB integration.

## Features

- RESTful API for product management
- MongoDB integration with Mongoose
- CORS enabled for frontend integration
- Product search and filtering
- Featured products endpoint
- Category-based product filtering
- Pagination support

## API Endpoints

### Products
- `GET /api/products` - Get all products (with optional filtering)
- `GET /api/products/featured` - Get featured products
- `GET /api/products/category/:category` - Get products by category
- `GET /api/products/:id` - Get single product
- `POST /api/products` - Create new product
- `PUT /api/products/:id` - Update product
- `DELETE /api/products/:id` - Delete product

### Health Check
- `GET /health` - Server health check

## Installation

1. Install dependencies:
```bash
npm install
```

2. Set up environment variables:
```bash
# Copy the example and modify as needed
cp .env.example .env
```

3. Build and start the server:
```bash
# Development (with auto-reload)
npm run dev

# Production build and start
npm run build
npm start

# Or start directly (if no build step needed)
npm start
```

## Environment Variables

- `MONGODB_URI` - MongoDB connection string
- `PORT` - Server port (default: 3001)
- `NODE_ENV` - Environment (development/production)
- `FRONTEND_URL` - Frontend URL for CORS (default: http://localhost:5173)

## Deployment

### Netlify Functions (Serverless)

This API can be deployed as Netlify Functions for serverless architecture:

1. **Setup Netlify Functions:**
   ```bash
   # Create netlify functions directory
   mkdir netlify/functions
   
   # Move server logic to a function
   cp server.js netlify/functions/products.js
   ```

2. **Configure netlify.toml:**
   ```toml
   [build]
     functions = "netlify/functions"
     command = "npm run build"
   
   [[redirects]]
     from = "/api/*"
     to = "/.netlify/functions/products"
     status = 200
   ```

3. **Deploy to Netlify:**
   - Connect your GitHub repository to Netlify
   - Set build command: `npm run build`
   - Set environment variables in Netlify dashboard:
     - `MONGODB_URI`
     - `NODE_ENV=production`
     - `FRONTEND_URL`

### Traditional Server Deployment

This server can also be deployed to any Node.js hosting platform like:
- Heroku
- Railway
- Render
- DigitalOcean App Platform
- AWS EC2
- Google Cloud Run
- Vercel

Make sure to set the environment variables in your deployment platform.

### Environment Variables for Deployment

Set these in your deployment platform:

```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/database
NODE_ENV=production
FRONTEND_URL=https://your-frontend-domain.com
PORT=3001
```

### Quick Deploy with Railway (Recommended)

1. Go to [Railway.app](https://railway.app)
2. Connect your GitHub account
3. Create a new project from GitHub
4. Select this repository
5. Railway will automatically detect it's a Node.js app
6. Configure build settings:
   - Build Command: `npm run build`
   - Start Command: `npm start`
7. Set environment variables in Railway dashboard
8. Deploy!

For detailed deployment instructions, see [DEPLOYMENT.md](./DEPLOYMENT.md).
