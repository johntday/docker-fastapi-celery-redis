FROM python:3.12-alpine

ENV CELERY_BROKER_URL redis://redis:6379/0
ENV CELERY_RESULT_BACKEND redis://redis:6379/0
ENV C_FORCE_ROOT true

ENV HOST 0.0.0.0
ENV PORT 5001
ENV DEBUG true

COPY . /api
WORKDIR /api

# install requirements

RUN pip install -U setuptools pip
RUN pip install -r freeze.txt

# expose the app port
EXPOSE 5001

RUN pip install uvicorn

# run the app server in production with gunicorn
CMD ["uvicorn", "--host", "0.0.0.0", "--port", "5001", "--workers", "3", "app:app"]