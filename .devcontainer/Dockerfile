# Nutze das volle Jupyter Data Science Notebook Image
FROM jupyter/datascience-notebook:latest

# Wechsle zu root, um Systempakete zu installieren
USER root

# Systempakete installieren (hier nur git)
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
 && apt-get clean && rm -rf /var/lib/apt/lists/*

# Zurück zum non-root NB_USER (jovyan)
USER ${NB_USER}

# Setze default shell für folgende Befehle
SHELL ["bash", "-c"]

# Optional: Upgrade pip zuerst (kann helfen)
RUN pip install --no-cache-dir --upgrade pip

# Requirements installieren (wenn du möchtest, kannst du das auch im postCreateCommand lassen)
# COPY requirements.txt ./requirements.txt
# RUN pip install --no-cache-dir -r requirements.txt
