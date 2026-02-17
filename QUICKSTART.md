# Quick Start Guide

This guide helps you get the harmonised site and Centrico LiveLab demo running locally in under 5 minutes.

## Prerequisites

- Docker and Docker Compose
- Python 3.7+ (for serving static files)
- Git

## Option 1: Full Stack (Website + API)

Perfect for testing the complete integration.

### Step 1: Clone and Set Up Repositories

```bash
# Create a workspace directory
mkdir neuromorphic-workspace
cd neuromorphic-workspace

# Clone both repositories
git clone https://github.com/nepryoon/neuromorphic-inference-lab-site.git
git clone https://github.com/nepryoon/centrico-livelab-mlops.git
```

### Step 2: Apply Changes

**For neuromorphic-inference-lab-site:**
```bash
cd neuromorphic-inference-lab-site

# Copy changes from workspace (if not already in repo)
# Or create a branch from the PR:
git fetch origin feature/harmonisation-and-centrico-integration
git checkout feature/harmonisation-and-centrico-integration
```

**For centrico-livelab-mlops:**
```bash
cd ../centrico-livelab-mlops

# Copy changes or checkout branch:
git fetch origin feature/cors-and-website-integration
git checkout feature/cors-and-website-integration
```

### Step 3: Start the API

```bash
cd centrico-livelab-mlops

# Start the inference API + database
docker compose -f docker-compose.local.yml -f docker-compose.data.yml up --build

# Wait for startup message: "Uvicorn running on http://0.0.0.0:8000"
```

**In a new terminal**, verify the API is working:
```bash
curl http://localhost:8000/health
# Should return: {"status":"healthy","model_loaded":true,"version":"..."}
```

### Step 4: Start the Website

```bash
cd neuromorphic-inference-lab-site

# Serve the static site
python -m http.server 8000

# Alternative: use any static file server
# npx serve -l 8000
```

### Step 5: Test the Integration

Open your browser:
- **Homepage**: http://localhost:8000/
  - Check: "Try data prep demo" button appears
- **Demos page**: http://localhost:8000/demos/
  - Check: Featured Open Banking card at top
- **Centrico demo**: http://localhost:8000/demos/centrico-livelab/
  - Check: "Live API Demo" section appears
  - Click "Check Health" - should show green status
  - Click "Get Prediction" - should return prediction result

## Option 2: Website Only

Test the CSS harmonisation and UI changes without running the API.

```bash
# Clone and serve
git clone https://github.com/nepryoon/neuromorphic-inference-lab-site.git
cd neuromorphic-inference-lab-site
python -m http.server 8000

# Visit http://localhost:8000
```

**What to check:**
- Consistent spacing between sections
- Homepage CTA button
- /demos/ featured card
- Navigation consistency across pages
- Footer with build provenance

The Centrico demo will show "API Offline" status, which is expected.

## Option 3: API Only

Test the Centrico LiveLab API with CORS support.

```bash
# Clone and start
git clone https://github.com/nepryoon/centrico-livelab-mlops.git
cd centrico-livelab-mlops
docker compose -f docker-compose.local.yml -f docker-compose.data.yml up --build

# Test endpoints
curl http://localhost:8000/health
curl http://localhost:8000/model
curl -X POST http://localhost:8000/predict -H "Content-Type: application/json" -d '{}'

# Check CORS headers
curl -H "Origin: https://example.com" -I http://localhost:8000/health
# Should include: Access-Control-Allow-Origin: *
```

## Troubleshooting

### API won't start
```bash
# Check Docker is running
docker ps

# Check ports aren't in use
lsof -i :8000
lsof -i :5432

# View logs
docker compose -f docker-compose.local.yml -f docker-compose.data.yml logs -f
```

### Website won't connect to API
```bash
# Verify API is responding
curl http://localhost:8000/health

# Check CORS headers
curl -H "Origin: http://localhost:8000" -v http://localhost:8000/health

# Open browser console (F12) and check for CORS errors
```

### "Model not loaded" in API
This is expected on first start. To load a model:

```bash
# Run training
cd centrico-livelab-mlops
docker compose -f docker-compose.local.yml -f docker-compose.data.yml -f docker-compose.train.yml run --rm trainer

# Restart inference service
docker compose -f docker-compose.local.yml restart inference
```

## Next Steps

### For Development
1. See [IMPLEMENTATION.md](./IMPLEMENTATION.md) for technical details
2. See [APPLY_CHANGES.md](./APPLY_CHANGES.md) for applying changes
3. Make your own modifications and test locally

### For Production
1. Deploy site to Cloudflare Pages
2. Set `CENTRICO_BASE_URL` environment variable
3. Deploy API with `ALLOWED_ORIGINS` configured
4. See deployment notes in [IMPLEMENTATION.md](./IMPLEMENTATION.md)

## Screenshots

### Homepage CTA Button
The "Try data prep demo" button appears prominently on the homepage action row.

### Featured Demo Card
On /demos/, the Open Banking Data Prep demo has a special card with gradient background at the top of the listing.

### Interactive Demo
The Centrico LiveLab page now includes:
- API status indicator (green when connected)
- Interactive prediction form
- Real-time results display
- Configuration status checker

## File Locations

If you need to modify the changes:

**CSS Harmonisation:**
- `neuromorphic-inference-lab-site/style.css` (lines 1-30: spacing tokens)

**CTA Buttons:**
- `neuromorphic-inference-lab-site/index.html` (line ~52)
- `neuromorphic-inference-lab-site/demos/index.html` (after line 55)

**API Proxy:**
- `neuromorphic-inference-lab-site/functions/api/centrico/*.js` (3 files)

**Interactive Demo:**
- `neuromorphic-inference-lab-site/demos/centrico-livelab/index.html` (after line 296)

**CORS Configuration:**
- `centrico-livelab-mlops/services/inference/app/main.py` (lines 28-45)

## Getting Help

- Full documentation: [IMPLEMENTATION.md](./IMPLEMENTATION.md)
- Change application: [APPLY_CHANGES.md](./APPLY_CHANGES.md)
- Project summary: [SUMMARY.md](./SUMMARY.md)
- GitHub Issues: [Create an issue](https://github.com/nepryoon/neuromorphic-inference-lab/issues)

## Success Checklist

Use this to verify your setup:

- [ ] API responds to http://localhost:8000/health
- [ ] Website serves at http://localhost:8000
- [ ] Homepage shows "Try data prep demo" button
- [ ] /demos/ page shows featured Open Banking card
- [ ] Centrico demo page loads without errors
- [ ] "Check Health" button returns green status
- [ ] "Get Prediction" button returns prediction
- [ ] CSS spacing looks consistent across pages
- [ ] Navigation works on all pages
- [ ] Footer displays build provenance

**All checked?** You're ready to use the harmonised site! 🎉
