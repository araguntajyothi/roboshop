FROM python:3.9-slim
EXPOSE 8080
USER root
WORKDIR /app
COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt  # Avoid caching unnecessary packages
COPY *.py /app/
COPY payment.ini /app/
CMD ["uwsgi", "--ini", "payment.ini"]


