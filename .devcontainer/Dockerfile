FROM jupyter/minimal-notebook:lab-4.3.6

USER root
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
 && apt-get clean && rm -rf /var/lib/apt/lists/*

USER ${NB_USER}

SHELL ["bash", "-c"]

RUN pip install --no-cache-dir uv==0.6.6
