FROM python3.9-alpine


# The installer requires curl (and certificates) to download the release archive
RUN apt-get update && apt-get install -y --no-install-recommends curl ca-certificates

# Download the latest installer
ADD https://astral.sh/uv/install.sh /uv-installer.sh

# Run the installer then remove it
RUN sh /uv-installer.sh && rm /uv-installer.sh

# Ensure the installed binary is on the `PATH`
ENV PATH="/root/.local/bin/:$PATH"


ENV CELERY_BROKER_URL redis://redis:6379/0
ENV CELERY_RESULT_BACKEND redis://redis:6379/0
ENV C_FORCE_ROOT true

ENV HOST 0.0.0.0
ENV PORT 5001
ENV DEBUG true

COPY . /api
WORKDIR /api

# install requirements

#RUN pip install -U setuptools pip
RUN uv pip install -r requirements.txt

# expose the app port
EXPOSE 5001

RUN uv pip install uvicorn

# run the app server in production with gunicorn
CMD ["uvicorn", "--host", "0.0.0.0", "--port", "5001", "--workers", "3", "app:app"]