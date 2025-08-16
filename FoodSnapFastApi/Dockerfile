# Use a lightweight official Python 3.10 image
FROM python:3.10-slim

# Set working directory inside the container
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender-dev \
    && rm -rf /var/lib/apt/lists/*

# Upgrade pip and setup tools


RUN pip install --upgrade pip setuptools wheel

# Copy requirements files
COPY requirement.txt requirement.txt
COPY requirement1.txt requirement1.txt

# Install dependencies from both requirement files
# Assumes you've updated torch/tensorflow versions in both files
RUN pip install --no-cache-dir -r requirement.txt
RUN pip install --no-cache-dir -r requirement1.txt

# Copy all project files into the container
COPY . .

# Expose FastAPI port
EXPOSE 8000

# Start FastAPI using uvicorn
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
