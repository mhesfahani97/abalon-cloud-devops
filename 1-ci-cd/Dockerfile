# security means hardening!
# using official image with minimal useless dependencies (goods for performance and security).
# don't use alpine Linux, that can lead to longer build times, obscure bugs, and performance issues.(based on experimental results).
# attention to version for being up to date for bug fixing.(goods for performance).
ARG PYTHON_VERSION=3.11.4
FROM python:${PYTHON_VERSION}-slim as base
# it is just for security and not performance (team lead check it!).
# combining commands to reduce layers and image size (good for performance).
RUN apt-get update && apt-get upgrade -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
# some important environment variables such passwords should not do hardcode
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app
# run application as non root user (security benefit).
# you can use remapping too! (team lead check it!).
ARG UID=10001
RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "/nonexistent" \
    --shell "/sbin/nologin" \
    --no-create-home \
    --uid "${UID}" \
    appuser
# you can don't combine it and use addition layer COPY for requirements
RUN --mount=type=cache,target=/root/.cache/pip \
    --mount=type=bind,source=requirements.txt,target=requirements.txt \
    python -m pip install -r requirements.txt

USER appuser

COPY . .

EXPOSE 5000

CMD python3 -m flask run --host=0.0.0.0
