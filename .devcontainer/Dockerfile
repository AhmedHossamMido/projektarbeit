FROM quay.io/jupyter/base-notebook:lab-4.3.6

USER root
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    debuginfod \
    build-essential \
 && rm -rf /var/lib/apt/lists/*

ENV DEBUGINFOD_URLS="https://debuginfod.ubuntu.com/"

USER jovyan
SHELL ["conda", "run", "--no-capture-output", "-n", "base", "/bin/bash", "-c"]

RUN pip install uv==0.6.6
