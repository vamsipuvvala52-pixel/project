# StockSeer AI — ML Stock Forecasting Platform

## 🚀 Deploy to Render (Step-by-Step)

### 1. Push to GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/stockseer-ai.git
git push -u origin main
```
> ⚠️ Make sure the `data/` folder is committed — it contains the CSV files needed for forecasts.

### 2. Deploy on Render
1. Go to [render.com](https://render.com) → **New** → **Web Service**
2. Connect your GitHub repo
3. Render will auto-detect settings from `render.yaml`
4. Set these manually if needed:
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `gunicorn app:app --timeout 120 --workers 1 --bind 0.0.0.0:$PORT`
5. Add environment variable: `SECRET_KEY` → any random string (or use "Generate Value")
6. Click **Deploy**

### 3. Verify Deployment
Visit `https://your-app.onrender.com/health` — should return:
```json
{"status": "ok", "tickers": ["AAPL", "AMZN", ...]}
```
If `tickers` is empty `[]`, the `data/` folder was not committed to Git.

---

## 🖥️ Run Locally

```bash
pip install -r requirements.txt
python app.py
# Open http://localhost:5000
```

## 🔐 Login Credentials
| Username | Password  | Role  |
|----------|-----------|-------|
| admin    | admin123  | Admin |
| demo     | demo123   | User  |

---

## 🔧 What Was Fixed for Render

| Problem | Fix |
|---------|-----|
| No Procfile | Added Procfile with gunicorn command |
| gunicorn missing | Added to requirements.txt |
| SECRET_KEY regenerated on restart | Now reads from SECRET_KEY env variable |
| PORT hardcoded to 5000 | Now reads $PORT env variable from Render |
| data/ folder not tracked in git | Added .gitignore that keeps data/ |
| No health check endpoint | Added /health route |
| No render.yaml | Added for one-click deployment config |
