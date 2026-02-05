# mini-feature-store
Production-style mini feature store with offline/online pipelines, metadata tracking, and monitoring

## Quick Start

Get the project running in **10 minutes**:

### Prerequisites
- Python 3.9+
- Docker & Docker Compose
- Git

### 1. Clone the Repository

```bash
git clone https://github.com/Vishnu633/mini-feature-store.git
cd mini-feature-store
```

### 2. Run Bootstrap (Sets Up Everything)

```bash
chmod +x scripts/bootstrap.sh
./scripts/bootstrap.sh
```

This will:
- ✅ Create Python virtual environment
- ✅ Install all dependencies
- ✅ Start Docker services (Redis, PostgreSQL, MinIO, Prometheus, Grafana)

### 3. Generate Data & Train Model

```bash
source .venv/bin/activate
PYTHONPATH=. python src/training/train.py --input data/raw/events.csv
```

### 4. Start API Server

```bash
PYTHONPATH=. uvicorn src.serving.api:app --port 8000
```

### 5. Test Prediction

```bash
# In another terminal
curl -X POST http://localhost:8000/predict \
  -H "Content-Type: application/json" \
  -d '{"user_id": "user_000050"}' | python -m json.tool
```

### 6. View Dashboards

- **Grafana**: http://localhost:3000 (admin/admin)
- **Prometheus**: http://localhost:9090
- **API Docs**: http://localhost:8000/docs

**That's it! You now have a working feature store.** 🎉
