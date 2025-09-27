# Deployment Guide for Products Inventory Server

## Quick Deploy Options

### Option 1: Railway (Recommended)
1. Go to [Railway.app](https://railway.app)
2. Connect your GitHub account
3. Create a new project from GitHub
4. Select the `productsInventory` repository
5. Railway will automatically detect it's a Node.js app
6. Set environment variables:
   - `MONGODB_URI`: Your MongoDB connection string
   - `NODE_ENV`: production
   - `FRONTEND_URL`: Your frontend URL (e.g., https://your-frontend.netlify.app)
7. Deploy!

### Option 2: Render
1. Go to [Render.com](https://render.com)
2. Create a new Web Service
3. Connect your GitHub repository
4. Select the `productsInventory` folder
5. Configure:
   - Build Command: `npm install`
   - Start Command: `npm start`
   - Environment: Node
6. Set environment variables (same as above)
7. Deploy!

### Option 3: Heroku
1. Install Heroku CLI
2. Login: `heroku login`
3. Create app: `heroku create your-products-server`
4. Set environment variables:
   ```bash
   heroku config:set MONGODB_URI="your-mongodb-uri"
   heroku config:set NODE_ENV="production"
   heroku config:set FRONTEND_URL="https://your-frontend.netlify.app"
   ```
5. Deploy: `git push heroku main`

## Environment Variables

Set these in your deployment platform:

```env
MONGODB_URI=mongodb+srv://admin_123:nhRb9NllTbzdEhuc@neweraproducts.wige5q7.mongodb.net/?retryWrites=true&w=majority&appName=NewEraProducts
NODE_ENV=production
FRONTEND_URL=https://your-frontend-domain.com
```

## Update Frontend

After deploying your server, update the frontend's API URL:

1. In your frontend project, create a `.env` file:
```env
VITE_API_URL=https://your-deployed-server.com/api
```

2. Or update the hardcoded URL in `src/contexts/ProductContext.tsx`:
```typescript
const API_BASE_URL = import.meta.env.VITE_API_URL || (import.meta.env.PROD ? 'https://your-deployed-server.com/api' : 'http://localhost:3001/api')
```

## Testing

After deployment, test your server:
```bash
curl https://your-deployed-server.com/health
curl https://your-deployed-server.com/api/products
```

## Remove Netlify Functions

Once the new server is deployed and working:
1. Delete the `netlify/functions` folder from your frontend project
2. Update `netlify.toml` to remove the functions configuration
3. Redeploy your frontend
