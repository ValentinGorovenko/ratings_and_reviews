FROM python:3.7-slim

WORKDIR /app

COPY /api_yamdb/requirements.txt .

RUN pip3 install -U pip
RUN pip3 install --no-cache-dir -r /app/requirements.txt

COPY /api_yamdb/ .

CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000" ]