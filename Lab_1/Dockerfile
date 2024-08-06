# Use a base image
FROM python:3.9-slim

# Set metadata
LABEL maintainer="your-email@example.com"

# Set environment variables
ENV PYTHONUNBUFFERED=1

# Set the working directory
WORKDIR /app

# Copy requirements.txt and install dependencies
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code to the container
COPY . .

# Expose a port
EXPOSE 8000

# Specify the command to run when the container starts
CMD ["python", "app.py"]
