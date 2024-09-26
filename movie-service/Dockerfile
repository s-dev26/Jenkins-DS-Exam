FROM python:3.8-slim


ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /movie-service


RUN apt-get update \
    && apt-get install -y gcc \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /root/.cache/pip


COPY . .


