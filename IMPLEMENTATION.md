# Site Harmonisation & Centrico LiveLab Integration — Implementation Summary

## Overview
This document tracks the implementation of site-wide harmonisation and Centrico LiveLab demo integration across two repositories:
1. `neuromorphic-inference-lab-site` - Website repository
2. `centrico-livelab-mlops` - MLOps inference API repository

## Changes Made

### A) Site Repository (`neuromorphic-inference-lab-site`)

#### 1. CSS Harmonisation (`style.css`)
- ✅ Added CSS spacing tokens for consistent vertical rhythm:
  - `--space-1: 8px`
  - `--space-2: 12px`
  - `--space-3: 16px`
  - `--space-4: 24px`
  - `--section-gap: 18px`
- ✅ Updated all hardcoded spacing values to use CSS custom properties
- ✅ Added utility classes: `.mt-1`, `.mt-2`, `.mt-3`, `.mt-4`, `.mb-2`
- ✅ Standardised spacing for: sections, cards, grids, badges, tags, buttons

#### 2. Navigation Consistency
- ✅ Fixed missing `.inner` wrapper in `demos/centrico-livelab/index.html`
- ✅ All pages now share identical nav structure with proper container wrapping

#### 3. CTA Buttons for Open Banking Demo
- ✅ Added prominent CTA button on homepage (`index.html`):
  - "Try data prep demo" button linking to `/demos/open-banking-data-prep/`
- ✅ Added featured demo card on `/demos/` page:
  - Highlighted card with gradient background at top of systems listing
  - Includes clear CTA and feature badges

#### 4. Cloudflare Pages Functions API Proxy (`functions/api/centrico/`)
- ✅ Created `health.js` - Proxies `/health` endpoint
- ✅ Created `model.js` - Proxies `/model` endpoint  
- ✅ Created `predict.js` - Proxies `/predict` endpoint (POST)
- ✅ Features:
  - CORS headers for browser access
  - Environment variable support (`CENTRICO_BASE_URL`)
  - Retry logic with exponential backoff
  - Helpful error messages for API not configured state
  - Timeout handling (20s for inference)
  - Fallback to localhost for local development

#### 5. Interactive Centrico LiveLab Demo (`demos/centrico-livelab/index.html`)
- ✅ Added "Live API Demo" section with:
  - API status indicator (connected/offline with visual badge)
  - Prediction options (DB mode or manual features)
  - Interactive buttons: Get Prediction, Check Health, Model Info
  - Results panel with formatted JSON output
  - Human-friendly prediction interpretation
  - Configuration status checker
- ✅ JavaScript functionality:
  - Async fetch calls to `/api/centrico/*` endpoints
  - Graceful error handling with user-friendly messages
  - Mode switching (DB vs manual features)
  - JSON validation for manual inputs
  - Automatic config check on page load

### B) Centrico LiveLab Repository (`centrico-livelab-mlops`)

#### 1. CORS Middleware (`services/inference/app/main.py`)
- ✅ Added FastAPI CORS middleware import
- ✅ Configured CORS with:
  - `ALLOWED_ORIGINS` environment variable support
  - Comma-separated origin list parsing
  - Default `*` for development
  - All methods and headers allowed
  - Credentials support enabled

#### 2. Documentation Updates (`README.md`)
- ✅ Added environment variables section documenting `ALLOWED_ORIGINS`
- ✅ Added "Exposing the API for Website Integration" section covering:
  - Local development setup
  - CORS configuration instructions
  - Production deployment notes (reverse proxy, timeouts, health checks)
  - Cloudflare Pages Function proxy example code
  - API contract examples with curl commands
- ✅ Maintained British English consistency throughout

## Testing & Validation

### Website Changes
To validate the website changes:

```bash
cd /path/to/neuromorphic-inference-lab-site

# For local development with Cloudflare Pages CLI (if available):
npx wrangler pages dev . --port 8788

# Or use any static server:
python -m http.server 8000
# Then visit: http://localhost:8000
```

Check:
- ✅ Consistent spacing between sections across all pages
- ✅ Navigation works and active states highlight correctly
- ✅ CTA buttons visible on homepage and /demos/ page
- ✅ Responsive layout works on mobile (no overlaps)
- ✅ Footer renders with build provenance

### Centrico LiveLab API
To validate the Centrico LiveLab changes:

```bash
cd /path/to/centrico-livelab-mlops

# Start the full stack:
docker compose \
  -f docker-compose.local.yml \
  -f docker-compose.data.yml \
  -f docker-compose.monitoring.yml \
  up --build

# In another terminal, test endpoints:
curl -s http://localhost:8000/health
curl -s http://localhost:8000/model
curl -X POST http://localhost:8000/predict -H "Content-Type: application/json" -d '{}'

# Visit interactive dashboard:
open http://localhost:8000/dashboard
```

Check:
- ✅ CORS headers present in responses
- ✅ Health endpoint returns model status
- ✅ Predict endpoint works with empty body (uses DB)
- ✅ Dashboard loads and displays charts

### End-to-End Integration
To validate the website calling the API:

**Option 1: Both services running locally**
```bash
# Terminal 1: Start Centrico LiveLab
cd /path/to/centrico-livelab-mlops
docker compose -f docker-compose.local.yml -f docker-compose.data.yml up

# Terminal 2: Start website
cd /path/to/neuromorphic-inference-lab-site
python -m http.server 8000

# Browser: Visit http://localhost:8000/demos/centrico-livelab/
# The API proxies will fall back to http://localhost:8000 automatically
```

**Option 2: Production (Cloudflare Pages)**
- Deploy website to Cloudflare Pages
- Set environment variable `CENTRICO_BASE_URL` to your deployed inference API URL
- Visit `/demos/centrico-livelab/` and test the interactive demo

## Files Changed Summary

### neuromorphic-inference-lab-site
```
style.css                                  (spacing tokens, utility classes)
index.html                                 (CTA button)
demos/index.html                           (featured demo card)
demos/centrico-livelab/index.html          (nav fix + interactive demo)
functions/api/centrico/health.js           (new proxy)
functions/api/centrico/model.js            (new proxy)
functions/api/centrico/predict.js          (new proxy)
```

### centrico-livelab-mlops
```
services/inference/app/main.py             (CORS middleware)
README.md                                  (integration docs)
```

## Deployment Notes

### Cloudflare Pages (Website)
1. Deploy `neuromorphic-inference-lab-site` repository
2. Set environment variable:
   - `CENTRICO_BASE_URL` = URL of deployed Centrico LiveLab inference API
3. Pages Functions will automatically proxy `/api/centrico/*` to the API

### Centrico LiveLab (Inference API)
1. Deploy using Docker Compose or container orchestration
2. Set environment variables:
   - `ALLOWED_ORIGINS` = `https://www.neuromorphicinference.com,https://neuromorphicinference.com`
   - `POSTGRES_HOST`, `POSTGRES_DB`, etc. (as per README)
3. Ensure `/health`, `/model`, `/predict` endpoints are accessible
4. Configure load balancer timeouts >= 30 seconds for inference endpoints

## Known Limitations & Future Work

### Not Implemented
- ❌ Changing `open-banking-data-prep` demo to call Centrico API (problem statement was ambiguous; existing demo is already functional)
- ❌ Authentication/API keys (not required for demo purposes)
- ❌ Rate limiting on API proxy
- ❌ Advanced monitoring/alerting integration in website

### Recommended Next Steps
1. Add Grafana dashboard embed in website demo page
2. Implement API key authentication for production
3. Add rate limiting to Cloudflare Functions
4. Create automated E2E tests for website → API flow
5. Add Prometheus metrics scraping from website (visitor analytics)

## Security Considerations

### CORS Configuration
- Development: CORS set to `*` (allow all origins)
- Production: Set `ALLOWED_ORIGINS` to specific domain(s)
- Website proxy adds additional CORS headers for redundancy

### API Exposure
- No authentication currently implemented
- Suitable for demo/portfolio purposes
- For production: Implement JWT tokens or API keys
- Consider Cloudflare Access for additional protection

### Environment Variables
- Never commit `CENTRICO_BASE_URL` or API keys to git
- Use Cloudflare Pages environment variables
- Use Docker Compose env files for local secrets

## Contact & Support

For questions about this implementation:
- GitHub: https://github.com/nepryoon
- Portfolio: https://www.neuromorphicinference.com/

## Appendix: Quick Reference

### API Proxy Endpoints (Website)
- `GET /api/centrico/health` → Inference API health check
- `GET /api/centrico/model` → Model metadata
- `POST /api/centrico/predict` → Prediction inference

### Centrico LiveLab Endpoints (Direct)
- `GET /health` → `{"status": "healthy", "model_loaded": true, "version": "..."}`
- `GET /model` → `{"version": "...", "features": [...]}`
- `POST /predict` → `{"y": 0|1, "proba": 0.0-1.0, "version": "..."}`
- `GET /dashboard` → Interactive MLOps dashboard (HTML)
- `GET /metrics` → Prometheus metrics (text)

### Useful Commands
```bash
# Site: Check spacing consistency
grep -r "margin\|padding" style.css | grep -v "var(--"

# API: Test CORS
curl -H "Origin: https://example.com" -I http://localhost:8000/health

# API: Check environment
docker compose -f docker-compose.local.yml exec inference env | grep ALLOWED

# Full stack restart
docker compose -f docker-compose.local.yml -f docker-compose.data.yml down
docker compose -f docker-compose.local.yml -f docker-compose.data.yml up --build
```
