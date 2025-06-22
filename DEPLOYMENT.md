# Deployment Guide for Render

## Prerequisites
1. A Render account (https://render.com)
2. Your code pushed to a GitHub repository
3. A Neon database (or other PostgreSQL database)

## Deployment Steps

### 1. Environment Variables
Set these environment variables in your Render service:

```
NODE_ENV=production
DATABASE_URL=your_neon_database_url
JWT_SECRET=your_jwt_secret_key
CLIENT_URL=https://your-app-name.onrender.com
```

### 2. Render Configuration
The app includes a `render.yaml` file that will automatically configure your service.

Alternatively, you can manually create a Web Service with these settings:
- **Build Command**: `npm install && npm run build`
- **Start Command**: `npm start`
- **Environment**: Node
- **Plan**: Free (or higher)

### 3. Database Setup
Make sure your Neon database is set up and the `DATABASE_URL` environment variable is configured.

Run database migrations if needed:
```bash
npm run db:push
```

### 4. WebSocket Configuration
The app is configured to handle WebSocket connections in production. The WebSocket server will run on the same port as your HTTP server.

### 5. Access Your App
Once deployed, your app will be available at:
- **Web Interface**: `https://your-app-name.onrender.com`
- **API Endpoints**: `https://your-app-name.onrender.com/api/*`
- **WebSocket**: `wss://your-app-name.onrender.com/ws`

## Local Development
For local development, use:
```bash
npm run dev
```

This will start both the client (port 5173) and server (port 5000) concurrently.

## Troubleshooting

### WebSocket Connection Issues
- Ensure your `CLIENT_URL` environment variable matches your deployed URL
- Check that the WebSocket path `/ws` is accessible
- Verify that your browser supports WebSocket connections

### Build Issues
- Make sure all dependencies are listed in `package.json`
- Check that the build commands complete successfully locally
- Verify that the `dist` directory is created after building

### Database Connection Issues
- Verify your `DATABASE_URL` is correct
- Ensure your database allows connections from Render's IP ranges
- Check that your database schema is up to date
