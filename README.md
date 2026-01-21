# MLOps Infrastructure Demo

A production-ready MLOps workflow demonstrating best practices in machine learning operations, from model training to deployment. This project showcases how to build a maintainable, scalable, and reproducible ML system.

## 🎯 Project Purpose

This project demonstrates **production-ready MLOps practices** rather than focusing solely on achieving state-of-the-art model performance. The goal is to showcase best practices in:

- **Reproducible ML Pipelines**: Using scikit-learn pipelines for consistent preprocessing and inference
- **API Design**: Building robust REST APIs with proper validation and error handling
- **Containerization**: Multi-service architecture with Docker Compose
- **CI/CD**: Automated quality gates, testing, and deployment pipelines
- **Code Quality**: Type checking, linting, and comprehensive testing

## 🔍 Why This Dataset?

The Wisconsin Breast Cancer dataset is used as a **proof-of-concept** to validate the MLOps infrastructure. This choice allows the project to focus on engineering practices rather than model complexity.

**Why not a more complex dataset?**
1. **Infrastructure First**: The same MLOps practices work for simple or complex models. The value is in the engineering, not the accuracy metric.
2. **Reproducibility**: A well-understood dataset ensures the infrastructure can be validated correctly before applying to more complex problems.
3. **Learning Focus**: This project started as a learning exercise to understand MLOps principles—using a simple dataset allows focus on infrastructure, not feature engineering.
4. **Transferability**: The practices demonstrated here are immediately applicable to any ML project, regardless of dataset complexity.

**The real question this project answers**: *"How do I ensure my ML model works the same way in production as it does in development?"*

## 🔧 What This Project Demonstrates

### 1. Modular & Testable ML Code
- **Separation of Concerns**: Clear boundaries between data ingestion, preprocessing, training, and inference
- **Unit Tests**: Comprehensive test coverage for each component (80%+ coverage requirement)
- **Integration Tests**: End-to-end testing of the full pipeline and API

### 2. Production-Ready API
- **Input Validation**: Pydantic schemas for strict type checking and validation
- **Error Handling**: Proper HTTP status codes and meaningful error messages
- **Logging**: Structured logging for debugging and monitoring
- **Health Checks**: Monitoring endpoints for service status

### 3. DevOps Best Practices
- **Docker Containerization**: Multi-stage builds for optimized image sizes
- **Docker Compose**: Orchestration of multi-service architecture
- **CI/CD Pipelines**: Automated testing, building, and deployment
- **Quality Gates**: Linting, type checking, and test coverage requirements before deployment

### 4. Reproducibility & Versioning
- **Locked Dependencies**: `uv.lock` ensures consistent environments
- **Versioned Pipelines**: Model artifacts tracked and reproducible
- **Documentation**: Clear setup and deployment instructions

## 🚀 Key Features

- ✅ **Type-Safe API**: Pydantic validation prevents production errors
- ✅ **Comprehensive Testing**: Unit and integration tests with 80%+ coverage
- ✅ **Automated CI/CD**: Quality gates ensure code quality before deployment
- ✅ **Multi-Container Setup**: Docker Compose for easy local development and deployment
- ✅ **Modern Python**: Type hints, dependency management with `uv`
- ✅ **Production-Ready**: Proper error handling, logging, and monitoring

## 📁 Project Structure

```
mlops-infrastructure-demo/
├── config/                    # Configuration files
│   ├── docker-compose.yml     # Multi-container Docker application
│   ├── Dockerfile.api         # Flask API container
│   └── Dockerfile.streamlit   # Streamlit UI container
├── data/                      # Dataset storage
│   └── data.csv
├── models/                    # Trained model artifacts
│   └── model.joblib
├── notebooks/                 # Exploratory analysis and experimentation
│   ├── 1.0-eda.ipynb
│   ├── 2.0-data_preprocessing.ipynb
│   ├── 3.0-feature_engineering.ipynb
│   └── 4.0-model_experimentation.ipynb
├── reports/                   # Generated reports and visualizations
│   ├── figures/
│   └── metrics/
├── src/                       # Source code
│   ├── app.py                 # Flask API for model inference
│   ├── schemas.py             # Pydantic schemas for API validation
│   ├── model/                 # ML pipeline components
│   │   ├── data_ingestion.py
│   │   ├── data_preprocessing.py
│   │   ├── model_inference.py
│   │   ├── model_training.py
│   │   └── pipeline_utils.py
│   └── streamlit_app.py       # Streamlit UI for predictions
├── tests/                     # Test suite
│   ├── unit/                  # Unit tests for each component
│   ├── integration/           # Integration tests
│   └── fixtures/              # Test data
├── .github/workflows/         # CI/CD workflows
│   └── main.yml
├── pyproject.toml             # Project dependencies (managed by uv)
├── requirements.txt           # Generated requirements for pip
└── uv.lock                    # Locked dependency versions
```

## 🛠️ Setup

### Prerequisites
- Python 3.12+
- Docker and Docker Compose (for containerized deployment)
- `uv` (recommended) or `pip` for dependency management

### Using `uv` (Recommended)

`uv` is a fast Python package installer written in Rust, offering faster dependency resolution and installation.

1. **Clone the repository:**
   ```bash
   git clone https://github.com/anibalrojosan/mlops-infrastructure-demo
   cd mlops-infrastructure-demo
   ```

2. **Install `uv` globally (if needed):**
   ```bash
   # On macOS/Linux:
   curl -LsSf https://astral.sh/uv/install.sh | sh
   # Or via pip:
   pip install uv
   ```

3. **Install dependencies:**
   ```bash
   uv sync --all-groups
   ```

4. **Activate the virtual env (optional):**
   ```bash
   source .venv/bin/activate
   ```

   Note: you can run commands using `uv run` if you don't want to activate the virtual env.

### Using `pip` (Alternative)


1. **Create and activate virtual environment:**
   ```bash
   python -m venv .venv
   # On Windows:
   .\.venv\Scripts\Activate.ps1
   # On Linux/macOS:
   source .venv/bin/activate
   ```

2. **Upgrade pip:**
   ```bash
   pip install --upgrade pip
   ```

3. **Install dependencies:**

   **Option A**: using the **requirements.txt** (recommended for production).

   ```
   pip install -r requirements.txt
   ```

   **Option B**: using the **pyproject.toml** (recommended for development).

   ```
   pip install .
   ```

## 🧪 Running Tests

The project includes comprehensive tests with a coverage requirement of 80%+.

**Run all tests:**
```bash
uv run pytest
```

**Run with verbose output:**
```bash
uv run pytest -v
```

**Run with coverage report:**
```bash
uv run pytest --cov=src --cov-report=term-missing
```

## 🚂 Training the Model

Train the ML pipeline and save the model artifact:

```bash
uv run python -m src.model.model_training
```

This will:
1. Load and preprocess the data
2. Train a Random Forest classifier within a scikit-learn pipeline
3. Evaluate the pipeline
4. Save the complete trained pipeline to `models/model.joblib`

**Note**: The model must be trained before running the API.

## 🌐 Running the API

Start the Flask API locally:

```bash
uv run python -m src.app
```

The API will be accessible at `http://127.0.0.1:5000/`

### API Endpoints

#### Health Check
```bash
GET http://127.0.0.1:5000/
```

**Response:**
```json
{
  "status": "healthy",
  "model_loaded": true
}
```

#### Prediction
```bash
POST http://127.0.0.1:5000/predict
Content-Type: application/json

{
  "radius_mean": 17.99,
  "texture_mean": 10.38,
  ...
}
```

**Response:**
```json
{
  "prediction": 1,
  "probability_benign": 0.1,
  "probability_malignant": 0.9
}
```

**Example using test scripts:**
- **Linux/macOS:** `./tests/integration/bash_test.sh`
- **Windows PowerShell:** `.\tests\integration\powershell_test.ps1`

## 🎨 Streamlit UI

The Streamlit application provides an interactive web interface for making predictions:

```bash
streamlit run src/streamlit_app.py
```

Ensure the Flask API is running first. The UI will open at `http://localhost:8501`.

## 🐳 Docker Deployment

The project uses Docker Compose to orchestrate both the Flask API and Streamlit UI services.

### Build and Run

```bash
docker compose -f config/docker-compose.yml up --build -d
```

This will:
- Build optimized images using multi-stage Docker builds
- Start both API and Streamlit services
- Make API available at `http://localhost:5000/`
- Make Streamlit UI available at `http://localhost:8501/`

### Stop Services

```bash
docker compose -f config/docker-compose.yml down
```

## 🔄 CI/CD Pipeline

The project includes a comprehensive CI/CD pipeline using GitHub Actions (`.github/workflows/main.yml`):

### Quality Gates Job
1. **Linting**: `ruff` for code style and quality
2. **Type Checking**: `mypy` for static type analysis
3. **Testing**: `pytest` with coverage reporting
4. **Coverage Requirement**: 80% minimum (pipeline fails if below)

### Build & Deploy Job (runs after quality gates pass)
1. **Train Model**: Train and save model artifact
2. **Build Docker Images**: Create optimized container images
3. **Push to Docker Hub**: Store images in registry
4. **Integration Testing**: Test services in isolated containers
5. **Health Checks**: Verify API and UI endpoints
6. **Cleanup**: Remove test containers

This ensures that only tested, validated code reaches production.

## 💡 Key Learnings & Transferability

This project demonstrates practices that are directly transferable to any ML project:

### What You Can Apply to Other Projects

1. **Pipeline Architecture**: The modular pipeline structure works for any ML problem
2. **API Design Patterns**: Pydantic validation and error handling are universal
3. **Testing Strategies**: Unit and integration test patterns
4. **CI/CD Practices**: Quality gates and automated deployment pipelines
5. **Containerization**: Docker setup that scales from development to production

### Real-World Applications

While this uses a simple dataset, these practices are used by:
- Teams deploying models to millions of users
- Companies managing hundreds of models in production
- Organizations requiring regulatory compliance (healthcare, finance)
- Startups building ML-first products

**The infrastructure scales regardless of model complexity.**

## 🔮 Future Improvements

Potential enhancements to further strengthen the MLOps workflow:

- **Model Versioning**: Implement MLFlow for experiment tracking and model registry
- **Monitoring**: Add model performance monitoring and drift detection
- **A/B Testing**: Framework for comparing model versions in production
- **Feature Store**: Centralized feature management for multiple models
- **Automated Retraining**: Scheduled retraining based on data drift or performance degradation

## 📚 Technologies Used

- **ML Framework**: scikit-learn
- **API Framework**: Flask
- **UI Framework**: Streamlit
- **Validation**: Pydantic
- **Testing**: pytest, pytest-mock
- **Containerization**: Docker, Docker Compose
- **CI/CD**: GitHub Actions
- **Code Quality**: ruff, mypy
- **Dependency Management**: uv

---

**Remember**: The value of this project is in the **engineering practices**, not the model metrics. These practices ensure your ML models work reliably in production, regardless of the problem domain or dataset complexity.
