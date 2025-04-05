FROM python:3.12-alpine

ENV CELERY_BROKER_URL redis://redis:6379/0
ENV CELERY_RESULT_BACKEND redis://redis:6379/0
ENV C_FORCE_ROOT true

COPY . /flower
WORKDIR /flower

RUN pip install -U setuptools pip
RUN pip install -r freeze.txt

# expose the app port
EXPOSE 5555

CMD["celery", "flower", "-A", "tasks"]
#    command:  ['celery', 'flower', '-A', 'tasks']
