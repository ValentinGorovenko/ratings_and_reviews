FROM python:3.7-slim
WORKDIR /api_yamdb
COPY /api_yamdb/requirements.txt .
RUN python -m pip install --upgrade pip
RUN pip install -r /api_yamdb/requirements.txt
COPY /api_yamdb/ .
CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000" ]