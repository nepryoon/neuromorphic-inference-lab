# Applying Changes from Multiple Repositories

This PR tracks work done across multiple repositories. The changes are documented in `IMPLEMENTATION.md`, but the actual code changes are in two separate repositories:

## Repositories with Changes

### 1. neuromorphic-inference-lab-site
**Repository:** https://github.com/nepryoon/neuromorphic-inference-lab-site

**Branch to create:** Create a new branch (e.g., `feature/harmonisation-and-centrico-integration`)

**Files to copy from this workspace:**

From `/home/runner/work/neuromorphic-inference-lab/neuromorphic-inference-lab-site/`:

```bash
# Modified files:
style.css
index.html
demos/index.html
demos/centrico-livelab/index.html

# New files:
functions/api/centrico/health.js
functions/api/centrico/model.js
functions/api/centrico/predict.js
```

**How to apply:**
```bash
# In your local clone of neuromorphic-inference-lab-site:
git checkout -b feature/harmonisation-and-centrico-integration

# Copy the modified files from the workspace
# (paths relative to workspace root)
cp /home/runner/work/neuromorphic-inference-lab/neuromorphic-inference-lab-site/style.css ./
cp /home/runner/work/neuromorphic-inference-lab/neuromorphic-inference-lab-site/index.html ./
cp /home/runner/work/neuromorphic-inference-lab/neuromorphic-inference-lab-site/demos/index.html ./demos/
cp /home/runner/work/neuromorphic-inference-lab/neuromorphic-inference-lab-site/demos/centrico-livelab/index.html ./demos/centrico-livelab/

# Create the API proxy functions
mkdir -p functions/api/centrico
cp /home/runner/work/neuromorphic-inference-lab/neuromorphic-inference-lab-site/functions/api/centrico/*.js ./functions/api/centrico/

# Commit and push
git add .
git commit -m "Harmonise site layout and add Centrico LiveLab integration"
git push origin feature/harmonisation-and-centrico-integration

# Create PR to main
```

### 2. centrico-livelab-mlops
**Repository:** https://github.com/nepryoon/centrico-livelab-mlops

**Branch to create:** Create a new branch (e.g., `feature/cors-and-website-integration`)

**Files to copy from this workspace:**

From `/home/runner/work/neuromorphic-inference-lab/centrico-livelab-mlops/`:

```bash
# Modified files:
services/inference/app/main.py
README.md
```

**How to apply:**
```bash
# In your local clone of centrico-livelab-mlops:
git checkout -b feature/cors-and-website-integration

# Copy the modified files
cp /home/runner/work/neuromorphic-inference-lab/centrico-livelab-mlops/services/inference/app/main.py ./services/inference/app/
cp /home/runner/work/neuromorphic-inference-lab/centrico-livelab-mlops/README.md ./

# Commit and push
git add .
git commit -m "Add CORS support and website integration documentation"
git push origin feature/cors-and-website-integration

# Create PR to main
```

## Alternative: Patches

If you prefer to use git patches instead of copying files:

### Generate patches from workspace

```bash
# For site repo:
cd /home/runner/work/neuromorphic-inference-lab/neuromorphic-inference-lab-site
git init
git add .
git commit -m "Site harmonisation changes"
git format-patch -1 HEAD --stdout > /tmp/site-changes.patch

# For centrico repo:
cd /home/runner/work/neuromorphic-inference-lab/centrico-livelab-mlops
git diff HEAD > /tmp/centrico-changes.patch
```

### Apply patches to your local repos

```bash
# In neuromorphic-inference-lab-site:
git checkout -b feature/harmonisation-and-centrico-integration
git apply /path/to/site-changes.patch
git commit -am "Apply site harmonisation changes"

# In centrico-livelab-mlops:
git checkout -b feature/cors-and-website-integration
git apply /path/to/centrico-changes.patch
git commit -am "Apply CORS and integration changes"
```

## Testing After Applying Changes

### Test the Website
```bash
cd neuromorphic-inference-lab-site
python -m http.server 8000
# Visit http://localhost:8000
```

Check:
- Homepage CTA button appears
- /demos/ page shows featured demo card
- CSS spacing is consistent
- Navigation works on all pages

### Test the API
```bash
cd centrico-livelab-mlops
docker compose -f docker-compose.local.yml -f docker-compose.data.yml up --build

# In another terminal:
curl -s http://localhost:8000/health
curl -X POST http://localhost:8000/predict -H "Content-Type: application/json" -d '{}'
```

### Test Integration
With both services running:
- Visit http://localhost:8000/demos/centrico-livelab/
- The interactive demo should connect to the API
- Try clicking "Check Health" and "Get Prediction"

## Deployment

### Deploy Website (Cloudflare Pages)
1. Merge PR in `neuromorphic-inference-lab-site`
2. Cloudflare Pages auto-deploys
3. Set environment variable: `CENTRICO_BASE_URL` → your API URL

### Deploy API
1. Merge PR in `centrico-livelab-mlops`
2. Deploy using your preferred method (Docker, ECS, etc.)
3. Set environment variable: `ALLOWED_ORIGINS` → your website domain(s)

See `IMPLEMENTATION.md` for detailed documentation.
