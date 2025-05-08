# Setting Up a Python FastAPI Virtual Environment with Virtualenv and Poetry
# Let's do it step by step. Directly execute the steps.

## Steps

### 1. Install `virtualenv`
If you haven't already, install `virtualenv` using pip:
```bash
pip install virtualenv
```

### 2. Create a Virtual Environment
Run the following command to create a new virtual environment:
```bash
python3 -m virtualenv ~/Desktop/coding/github/.fastapi_venv
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

### 6. Install Dependencies
Navigate to your project directory and install the required dependencies for your FastAPI project:
```bash
poetry add fastapi uvicorn pytest
```

### 7. Additional Configuration (Optional)
- **Set Up Pre-commit Hooks**:
  Install `pre-commit` to ensure code quality:
  ```bash
  poetry add --dev pre-commit
  pre-commit install
  ```
- **Add Linting and Formatting Tools**:
  Install tools like `flake8` and `black` for linting and formatting:
  ```bash
  poetry add --dev flake8 black
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

### 8. Run the FastAPI Application
Use `uvicorn` to run your FastAPI application:
```bash
uvicorn backend.src.fastapi:app --reload
```
- Replace `backend.src.fastapi:app` with the actual module and application instance name in your project if different.

### 9. Testing
Run your tests using `pytest`:
```bash
pytest
```

By following these steps, you will have a fully configured FastAPI project with a virtual environment and Poetry for dependency management.