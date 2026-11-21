FROM python:3.9-slim

WORKDIR /app
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

COPY requirements.txt ./requirements.txt
RUN pip install --no-cache-dir -r requirements.txt gunicorn==20.1.0

COPY . .
RUN mkdir -p /app/collected_static /app/media

CMD ["sh", "-c", "python manage.py migrate && python manage.py collectstatic --noinput && cp -r /app/collected_static/. /backend_static/ && gunicorn --bind 0.0.0.0:8000 kittygram_backend.wsgi:application"]
