FROM python:3.9-slim

WORKDIR /app

# Устанавливаем зависимости для работы с PostgreSQL и компиляции некоторых пакетов, если они понадобятся
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Копируем и устанавливаем зависимости Python
COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip && \
    pip install -r requirements.txt --no-cache-dir

# Копируем весь код приложения
COPY . .

# Запускаем production-сервер gunicorn на порту 8000
CMD ["gunicorn", "kittygram_backend.wsgi:application", "--bind", "0.0.0.0:8000"]