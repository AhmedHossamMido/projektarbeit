FROM jupyter/minimal-notebook:lab-4.3.6

USER root

# Installiere nur unbedingt nötige Pakete, ohne unnötige Recommends
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER ${NB_USER}

# Verwende die Shell wie von Codespaces/Jupyter erwartet
SHELL ["bash", "-c"]

# Installiere Python-Pakete (hier: 'uv') schlank
RUN pip install --no-cache-dir uv==0.6.6
