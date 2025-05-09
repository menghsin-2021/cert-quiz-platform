# Setting Up a Python FastAPI Virtual Environment with Virtualenv and Poetry
# Let's do it step by step. Directly execute the steps.

# This guide will help you set up a Python FastAPI virtual environment using `virtualenv` and `poetry` for dependency management.
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

### 1. Install `virtualenv`
If you haven't already, install `virtualenv` using pip:
```bash
python -m pip install --user --upgrade pip
pip install virtualenv
```

### 2. Create a Virtual Environment
Run the following command to create a new virtual environment:
```bash
python -m virtualenv ~/Desktop/coding/github/.fastapi_venv
```
- This command creates a new virtual environment in the specified directory. You can change the path as per your requirement.

### 3. Activate the Virtual Environment
- On macOS and Linux:
  ```bash
  source ~/Desktop/coding/github/.fastapi_venv/bin/activate
  ```
- On Windows:
  ```bash
  .\Desktop\coding\github\.fastapi_venv\Scripts\activate
  ```

### 4. Install `poetry`
If you haven't already, install `poetry` using pip:
```bash
pip install poetry
```

### 5. Configure Poetry to Use the Existing Virtual Environment
To disable Poetry from creating its own virtual environment, run:
```bash
poetry config virtualenvs.create false
```

### 6. Create a New FastAPI Project
Navigate to your desired directory and create a new FastAPI project using Poetry:
```bash
poetry new backend --src
```
- This command creates a new directory named `backend` with a `src` subdirectory, which will contain your FastAPI project.


### 7. Install Dependencies
Navigate to your project directory and install the required dependencies for your FastAPI project:
```bash
cd backend && poetry add fastapi uvicorn pytest
```

### 8. Additional Configuration (Optional)
- **Set Up Pre-commit Hooks**:
  Install `pre-commit` to ensure code quality:
  ```bash
  poetry add --dev pre-commit
  pre-commit install
  ```
- **Add Linting and Formatting Tools**:
  Install tools like `flake8`, `black`, and `isort` for linting and formatting:
  ```bash
  poetry add --dev flake8 black isort
  ```
- **Set Up Environment Variables**:
  Create a `.env` file in your project directory to manage sensitive information:
  ```bash
  touch .env
  ```
  Add your environment variables to the `.env` file and use a library like `python-dotenv` to load them:
  ```bash
  poetry add python-dotenv
  ```
- **Create a `.pre-commit-config.yaml` file**:
  ```bash
  touch .pre-commit-config.yaml
  ```
  Add the following code to the `.pre-commit-config.yaml` file:
  ```yaml
  repos:
    - repo: https://github.com/pre-commit/pre-commit
      rev: v2.13.0
      hooks:
        - id: flake8
        - id: black

  - repo: https://github.com/pre-commit/mirrors-isort
    rev: v5.10.1
    hooks:
      - id: isort
  ```
  - This configuration will run `flake8`, `black`, and `isort` on your code before each commit.

- **Create Basic setting for flake8 and black in pyproject.toml**
  - Add the following code to your `pyproject.toml` file:
    ```
    [tool.flake8]
    max-line-length = 88
    extend-ignore = ["E203", "W503"]
    [tool.black]
    line-length = 88
    skip-string-normalization = true
    [tool.isort]
    profile = "black"
    line_length = 88
    known_third_party = ["fastapi"]
    ```
- This configuration sets the maximum line length for `flake8` and `black` to 88 characters, which is the default for `black`.

- **Create a `.gitignore` file**:
  ```bash
  touch .gitignore
  ```
  Add the following code to the `.gitignore` file for ignoring unnecessary files:
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

### 9. Create a Basic FastAPI Application
Create a `main.py` file under `backend/src/` in your project directory and add the following code:
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}
```

### 10. Run the FastAPI Application
Use `uvicorn` to run your FastAPI application:
```bash
uvicorn backend.src.main:app --reload
```
- Replace `backend.src.main:app` with the actual module and application instance name in your project if different.


### 11. Create a Test File
Create a `test_main.py` file in your project directory and add the following code:
```python
from fastapi.testclient import TestClient
from .main import app
client = TestClient(app)
def test_read_root():
    response = client.get("/")
    assert response.status_code == 200
    assert response.json() == {"Hello": "World"}
```
- This test checks if the root endpoint returns a 200 status code and the expected JSON response.

### 12. Run the Tests
Run your tests using `pytest`:
```bash
pytest
```
- This command will discover and run all the tests in your project.


By following these steps, you will have a fully configured FastAPI project with a virtual environment and Poetry for dependency management.