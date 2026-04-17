FROM python:3.12.11-alpine3.22

RUN apk add --no-cache --virtual .build-deps gcc libc-dev linux-headers make \
 && apk add --no-cache bash git gettext libpq-dev libmagic

WORKDIR /app

COPY local_deps/ /app/local_deps/
COPY adapters.requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r /app/requirements.txt

RUN apk del --no-network .build-deps

ENV PYTHONUNBUFFERED=1
ENV GEN2_MASTER_DATA_API_WORKER_TYPE=gunicorn
ENV GEN2_MASTER_DATA_API_HOST=0.0.0.0
ENV GEN2_MASTER_DATA_API_PORT=8000
ENV GEN2_MASTER_DATA_API_NO_OF_WORKERS=8

# Use module path for migrate and Gunicorn WSGI app
CMD python3 -m openg2p_gen2_master_data.main migrate; \
    ${GEN2_MASTER_DATA_API_WORKER_TYPE} "openg2p_gen2_master_data.main:app" --workers ${GEN2_MASTER_DATA_API_NO_OF_WORKERS} --worker-class uvicorn.workers.UvicornWorker --bind ${GEN2_MASTER_DATA_API_HOST}:${GEN2_MASTER_DATA_API_PORT}