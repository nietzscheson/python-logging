FROM python:3.9 AS base

ENV PYTHONUNBUFFERED 1

RUN apt-get update \
    && apt-get install wget \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add -

RUN echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-7.x.list

RUN apt-get update && apt-get install filebeat

RUN service filebeat start

RUN pip3 install --upgrade pip awscli --upgrade --user --no-warn-script-location

RUN cp /root/.local/bin/aws /usr/bin/aws && chmod -R a+w /usr/bin/aws

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .