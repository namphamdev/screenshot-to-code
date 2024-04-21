FROM python:3.12-slim-bullseye

ENV POETRY_VERSION 1.4.1

# Install system dependencies
RUN pip install "poetry==$POETRY_VERSION"

# Set work directory
WORKDIR /app

# Copy only requirements to cache them in docker layer
COPY ./backend/poetry.lock ./backend/pyproject.toml /app/

# Disable the creation of virtual environments
RUN poetry config virtualenvs.create false

# Install dependencies
RUN poetry install

# Copy the current directory contents into the container at /app
COPY ./backend /app/
# RUN poetry run uvicorn main:app --host 0.0.0.0 --port 7001
CMD ["gunicorn", "-k", "uvicorn.workers.UvicornWorker", "main:app", "--bind", "0.0.0.0:8000"]

