# Use Python 3.9 as the base image
FROM python:3.9

# Expose port 8080
EXPOSE 8080

# Run as root user to install packages
USER root

# Set the working directory in the container
WORKDIR /app

# Copy the requirements.txt to the working directory
COPY requirements.txt /app/

# Install system dependencies needed for uwsgi and Python packages
RUN apt-get update && apt-get install -y \
    gcc \
    python3-dev \
    build-essential \
    libssl-dev \
    && pip install --no-cache-dir -r requirements.txt \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Copy the Python source code to the container
COPY *.py /app/

# Copy the uwsgi configuration file
COPY payment.ini /app/

# Set the command to run uwsgi with the specified ini file
CMD ["uwsgi", "--ini", "payment.ini"]
