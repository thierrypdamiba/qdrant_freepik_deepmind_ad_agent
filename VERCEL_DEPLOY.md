# Deploying to Vercel

This guide will help you deploy the Ad Generation Agent frontend to Vercel.

## Prerequisites

1. A Vercel account (sign up at https://vercel.com)
2. The Vercel CLI installed: `npm i -g vercel`
3. Your backend API deployed (see Backend Deployment section)

## Frontend Deployment

### Option 1: Deploy via Vercel Dashboard

1. Go to https://vercel.com/new
2. Import your GitHub repository: `thierrypdamiba/monday`
3. Configure the project:
   - **Root Directory**: `frontend`
   - **Framework Preset**: Next.js
   - **Build Command**: `npm run build`
   - **Output Directory**: `.next`
4. Add Environment Variables:
   - `NEXT_PUBLIC_API_URL`: Your backend API URL (e.g., `https://your-backend.railway.app` or `https://your-backend.render.com`)
5. Click "Deploy"

### Option 2: Deploy via CLI

```bash
cd frontend
vercel
```

Follow the prompts and add the `NEXT_PUBLIC_API_URL` environment variable when asked.

## Backend Deployment

The FastAPI backend needs to be deployed separately. Recommended options:

### Option A: Railway (Recommended)

1. Sign up at https://railway.app
2. Create a new project
3. Connect your GitHub repo
4. Add a new service from GitHub
5. Configure:
   - **Root Directory**: `/` (root)
   - **Start Command**: `python api.py` or `uvicorn api:app --host 0.0.0.0 --port $PORT`
   - **Environment Variables**: Add all from your `.env` file:
     - `QDRANT_URL`
     - `QDRANT_API_KEY`
     - `GOOGLE_API_KEY` or `GEMINI_API_KEY`
     - `FREEPIK_API_KEY`
6. Railway will provide a URL like `https://your-app.railway.app`
7. Update `NEXT_PUBLIC_API_URL` in Vercel to point to this URL

### Option B: Render

1. Sign up at https://render.com
2. Create a new Web Service
3. Connect your GitHub repo
4. Configure:
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `uvicorn api:app --host 0.0.0.0 --port $PORT`
   - **Environment Variables**: Add all from your `.env` file
5. Render will provide a URL
6. Update `NEXT_PUBLIC_API_URL` in Vercel

### Option C: Fly.io

1. Install Fly CLI: `curl -L https://fly.io/install.sh | sh`
2. Create `fly.toml` in project root
3. Run `fly launch` and follow prompts
4. Add environment variables: `fly secrets set KEY=value`
5. Deploy: `fly deploy`

## Environment Variables

### Frontend (Vercel)
- `NEXT_PUBLIC_API_URL`: Backend API URL (required)

### Backend (Railway/Render/Fly.io)
- `QDRANT_URL`: Your Qdrant cluster URL
- `QDRANT_API_KEY`: Your Qdrant API key
- `GOOGLE_API_KEY` or `GEMINI_API_KEY`: Google Gemini API key
- `FREEPIK_API_KEY`: Freepik API key
- `GEMINI_AGENT_MODEL`: (Optional) Model name, defaults to `gemini-2.0-flash-exp`

## Post-Deployment

1. Update CORS in `api.py` to allow your Vercel domain:
   ```python
   allow_origins=["https://your-app.vercel.app"]
   ```

2. Test the deployment:
   - Visit your Vercel URL
   - Try creating an ad
   - Check browser console for any errors

## Troubleshooting

- **CORS errors**: Make sure backend CORS allows your Vercel domain
- **API not found**: Verify `NEXT_PUBLIC_API_URL` is set correctly in Vercel
- **Build fails**: Check that all dependencies are in `package.json`
- **Backend timeout**: Increase timeout limits in your hosting provider

