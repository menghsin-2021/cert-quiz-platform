# Setting Up a Python FastAPI Virtual Environment with Poetry
# Let's do it step by step. Directly execute the steps.
# ask whether to proceed with the optional steps
# This guide will help you set up a Python FastAPI virtual environment using `poetry` for dependency management.
# The project structure will be as follows:
```
backend
├── poetry.lock
├── pyproject.toml
├── src
│   └── __init__.py
│   └── main.py
└── tests
    ├── __init__.py
    └── test_main.py
```
# The `src` directory will contain your FastAPI application, and the `tests` directory will contain your test files.
# The `poetry.lock` file will be generated automatically when you install dependencies using `poetry`.
# The `pyproject.toml` file will contain the configuration for your project, including dependencies and settings for tools like `black`, `flake8`, and `isort`.
# The `__init__.py` files are used to mark directories as Python packages.
# The `main.py` file will contain your FastAPI application code, and the `test_main.py` file will contain your test cases.

## Steps

### 1. Install `poetry`
If you haven't already, install `poetry` using pip:
```bash
pip install poetry
```

### 2. Create a New FastAPI Project
Navigate to your desired directory and create a new FastAPI project using Poetry:
```bash
poetry new backend --src
```
- This command creates a new directory named `backend` with a `src` subdirectory, which will contain your FastAPI project.

### 3. Navigate to the Project Directory
Change to the newly created project directory:
```bash
cd backend
```

### 4. Install Dependencies
According to the user's Python version, install the corresponding package versions:
- If using Python 3.8:
  ```bash
  poetry add fastapi uvicorn@0.17.0 pytest python-dotenv@0.21.0 httpx
  ```
- If using Python 3.9 or higher:
  ```bash
  poetry add fastapi uvicorn pytest python-dotenv httpx
  ```

### 5. Activate the Poetry Environment
Activate the virtual environment managed by Poetry:
```bash
poetry env use python && poetry env activate
source /Users/menghsin/Library/Caches/pypoetry/virtualenvs/backend-GwDCVs05-py3.12/bin/activate
```

### 6. Additional Configuration (Optional), must ask the user whether to proceed
- **Set Up Pre-commit Hooks**:
  Install `pre-commit` to ensure code quality：
  ```bash
  # If using Python 3.8
  poetry add --dev pre-commit@2.20.0

  # If using Python 3.9 or higher
  poetry add --dev pre-commit
  ```
  pre-commit install

- **Add Linting and Formatting Tools**:
  Install tools like `flake8`, `black`, and `isort` for code linting and formatting:
  ```bash
  # If using Python 3.8
  poetry add --dev flake8@5.0.4 black@22.3.0 isort@5.10.1

  # If using Python 3.9 or higher
  poetry add --dev flake8 black isort
  ```

- **Set Up Environment Variables**:
  Create a `.env` file in your project directory to manage sensitive information:
  ```bash
  touch .env
  ```
  Add your environment variables to the `.env` file and use the `python-dotenv` library to load them:
  ```bash
  poetry add python-dotenv@0.21.0
  ```

- **Create a `.pre-commit-config.yaml` file**:
  ```bash
  touch .pre-commit-config.yaml
  ```
  Add the following content to the `.pre-commit-config.yaml` file：
  ```yaml
  repos:
  - repo: local
    hooks:
      - id: isort
        name: Sort imports
        types: [python]
        entry: isort .
        language: system
      - id: black
        name: Black
        types: [python]
        entry: black .
        language: system
      - id: flake8
        name: Flake8
        types: [python]
        entry: flake8 .
        language: system
  ```
  - This configuration will run `flake8`, `black`, and `isort` before every commit.

- **Add Basic Settings for black and isort in pyproject.toml**:
  - Add the following content to the `pyproject.toml` file：
    ```
    [tool.black]
    line-length = 88
    skip-string-normalization = true
    [tool.isort]
    profile = "black"
    line_length = 88
    known_third_party = ["fastapi"]
    ```
  - This configuration sets the maximum line length for `flake8` and `black` to 88 characters, which is the default for `black`。

  - Add the following content to the `.flake8` file：
    ```ini
    [flake8]
    max-line-length = 88
    extend-ignore = E203, W503
    ```
- **Create a `.gitignore` file**:
  ```bash
  touch .gitignore
  ```
  Add the following content to the `.gitignore` file to ignore unnecessary files：
  ```gitignore
  .venv/
  __pycache__/
  *.pyc
  *.pyo
  *.pyd
  .env
  .pytest_cache/
  .mypy_cache/
  ```

- **Should this step be executed?**
  Please confirm whether this step is necessary; otherwise, it can be skipped。

### 7. Create a Basic FastAPI Application
Create a `main.py` file under `backend/src/` in your project directory and add the following code:
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}
```

### 8. Create a Test File
Create a `test_main.py` file in your project directory and add the following code:
```python
from fastapi.testclient import TestClient
from src.main import app
client = TestClient(app)
def test_read_root():
    response = client.get("/")
    assert response.status_code == 200
    assert response.json() == {"Hello": "World"}
```
- This test checks if the root endpoint returns a 200 status code and the expected JSON response.

### 9. Run the Tests
Run your tests using `pytest`:
```bash
pytest tests
```
- This command will discover and run all the tests in your project.

### 10. Run the FastAPI application
Then run the FastAPI application using `uvicorn`, do not open a new terminal:
```bash
uvicorn src.main:app --reload
```
- The `--reload` flag enables auto-reload, which is useful during development.

By following these steps, you will have a fully configured FastAPI project with Poetry for dependency management.