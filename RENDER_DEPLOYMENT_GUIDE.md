# VoiceConnect - Render Deployment Guide

## Quick Deploy to Render

### Method 1: GitHub Repository (Recommended)

1. **Upload to GitHub:**
   - Create a new repository on GitHub
   - Upload your VoiceConnect source code to the repository

2. **Deploy on Render:**
   - Go to [render.com](https://render.com) and sign up/login
   - Click "New +" → "Web Service"
   - Connect your GitHub repository
   - Use these settings:
     - **Name**: voiceconnect (or your preferred name)
     - **Environment**: Node
     - **Root Directory**: Leave empty (use repository root)
     - **Build Command**: `npm ci && npm run build`
     - **Start Command**: `npm start`
     - **Instance Type**: Free (or paid for better performance)

3. **Configure Environment:**
   - No additional environment variables needed
   - Render automatically provides PORT variable

### Method 2: Direct Upload

1. **Prepare Your Code:**
   - Ensure you have the `render.yaml` file in your project root
   - This file configures automatic deployment

2. **Create Web Service:**
   - Go to Render dashboard
   - Click "New +" → "Web Service"
   - Choose "Deploy an existing image or build from a Git repository"
   - Upload your source code directly

## Important Notes for Render

### HTTPS and WebRTC
- Render automatically provides HTTPS for all deployments
- This is required for WebRTC to work properly in browsers
- Your app will be accessible at: `https://your-app-name.onrender.com`

### WebSocket Support
- Render fully supports WebSocket connections
- No additional configuration needed for the signaling server

### Performance Considerations
- **Free Tier**: Service sleeps after 15 minutes of inactivity
- **Paid Tier**: Always available with better performance
- Consider upgrading for production use

### Domain and SSL
- Render provides free SSL certificates
- You can add custom domains in paid plans
- All connections are automatically secured

## Testing Your Deployment

1. **Access Your App:**
   - Visit your Render URL: `https://your-app-name.onrender.com`
   - Allow microphone permissions when prompted

2. **Test Voice Calling:**
   - Open the app in two different browser tabs/windows
   - Note the User ID in each tab
   - Use one tab to call the other using the User ID
   - Accept the call to test voice communication

## Troubleshooting

### Common Issues:

#### "Could not read package.json" Error:
- **Problem**: Render can't find package.json in expected location
- **Solution**: Ensure "Root Directory" is empty (use repository root)
- **Alternative**: Make sure package.json is in the top level of your repository

#### Build Command Issues:
- **Use**: `npm ci && npm run build` (standard build process)
- **Vite Build Error**: If you see "Rollup failed to resolve import" errors, this is typically due to path resolution
- **Solution**: Ensure all files are uploaded to GitHub correctly and package.json is in root directory
- **Node version**: Render uses Node 18+ by default (compatible with your app)
- **Alternative**: If build continues to fail, try manual deployment method below

#### App Won't Start:
- **Verify start command**: Must be exactly `npm start`
- **Check logs**: View deployment logs in Render dashboard for errors
- **Port binding**: App automatically uses Render's provided PORT variable

#### Voice Calling Issues:
- **No voice**: Ensure microphone permissions are granted in browser
- **Connection fails**: Verify both users are on HTTPS (Render provides this automatically)
- **WebSocket errors**: Check that app is deployed successfully and running

### Support:
- Check Render logs in your dashboard for error details
- Render documentation: [render.com/docs](https://render.com/docs)

## Cost Information

- **Free Tier**: 750 hours/month (sleeps after inactivity)
- **Starter**: $7/month (always available)
- **Standard**: $25/month (better performance)

Your VoiceConnect app is ready for Render deployment with all necessary configurations included!