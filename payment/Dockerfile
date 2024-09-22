# Use Python 3.9 slim image as the base
FROM python:3.9-slim

# Expose the application port
EXPOSE 8080

# Run as root user to install packages
USER root

# Set the working directory
WORKDIR /app

# Copy the requirements.txt file
COPY requirements.txt /app/

# Install build dependencies and uwsgi system dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    python3-dev \
    musl-dev \
    build-essential \
    libssl-dev \
    && pip install --no-cache-dir -r requirements.txt \
    && apt-get remove -y gcc python3-dev musl-dev build-essential libssl-dev \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Copy the Python source code
COPY *.py /app/

# Copy the uwsgi configuration file
COPY payment.ini /app/

# Set the command to run the uwsgi server
CMD ["uwsgi", "--ini", "payment.ini"]
