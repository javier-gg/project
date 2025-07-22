## Start from the Python 3.13 image based on Debian 11
FROM python:3.13-bullseye

## Avoid warnings by switching to noninteractive - may turn off later
ENV DEBIAN_FRONTEND=noninteractive

## Install Python
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    git \
    vim \
    && rm -rf /var/lib/apt/lists/*

## Install pandoc, pandoc-citeproc, and dependencies for Quarto
RUN apt-get update && apt-get install -y --no-install-recommends \
    pandoc \
    pandoc-citeproc \
    curl \
    gdebi-core \
    && rm -rf /var/lib/apt/lists/*

## Download and install Quarto and clean up in the same layer
RUN curl -LO https://quarto.org/download/latest/quarto-linux-amd64.deb \
    && gdebi --non-interactive quarto-linux-amd64.deb \
    && rm -f quarto-linux-amd64.deb

## Use pip to install needed packages
COPY requirements.txt /app/requirements.txt
WORKDIR /app
RUN pip install --upgrade pip
RUN pip install -r /app/requirements.txt

WORKDIR /workspace

EXPOSE 8888

CMD ["bash"]