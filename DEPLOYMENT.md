# Deployment Guide for Mind to Video

## Prerequisites
- An account on [Render.com](https://render.com/)
- OpenAI API key
- Runway API key
- The application ZIP file (mind_to_video.zip)

## Option 1: Deploy using Render.com and GitHub

1. **Fork or clone this repository**
   - This repository contains the necessary deployment files

2. **Create a new Web Service on Render**
   - Go to your Render dashboard
   - Click "New +" and select "Web Service"
   - Connect your GitHub repository

3. **Configure your service**
   - Name: `mind-to-video` (or your preferred name)
   - Environment: `Docker`
   - Branch: `master` (or your main branch)
   - Region: Choose the closest to your users
   - Plan: Select according to your needs (Free tier works for testing)

4. **Set Environment Variables**
   - `OPENAI_API_KEY`: Your OpenAI API key
   - `RUNWAY_API_KEY`: Your Runway API key
   - `SECRET_KEY`: A random string for Flask sessions
   - `ENVIRONMENT`: Set to "production"
   - `PORT`: Set to 10000

5. **Deploy**
   - Click "Create Web Service"
   - Wait for the deployment to complete

## Option 2: Manual Deployment

1. **Download the ZIP file**
   - Get the full application ZIP file (mind_to_video.zip)

2. **Extract the ZIP file**
   - Extract to your preferred location

3. **Set up environment variables**
   - Create a `.env` file with the required variables:
     ```
     OPENAI_API_KEY=your_openai_api_key
     RUNWAY_API_KEY=your_runway_api_key
     SECRET_KEY=your_secret_key
     ENVIRONMENT=production
     ```

4. **Run with Docker**
   ```
   docker build -t mind-to-video .
   docker run -p 8080:8080 --env-file .env mind-to-video
   ```

5. **Or run directly with Python**
   ```
   pip install -r requirements.txt
   gunicorn app:app --bind 0.0.0.0:8080
   ```

## Accessing Your Deployed Application

Once deployed, your application will be available at the URL provided by Render.
For local deployments, access at http://localhost:8080

## Troubleshooting

- **WebSocket Issues**: Ensure your deployment platform supports WebSocket connections
- **API Rate Limits**: Check your OpenAI and Runway API usage if generation fails
- **Memory Errors**: Increase container memory if you encounter out-of-memory errors
