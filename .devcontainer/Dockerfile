# syntax=docker/dockerfile:1
# https://docs.docker.com/reference/dockerfile/#syntax

## Build the container image
# docker build . -t scipro --progress plain
# podman build . -t scipro --progress=plain --format=docker

## Run the container image, port 8888 for jupyterlab, port 9001 for viztracer (optional)
# Note: "--IdentityProvider.token=" is dangerous, but convenient (no need to copy the token from the terminal)
# docker run --rm --name scipro -p 8888:8888 -p 9001:9001 --mount type=bind,source="$(pwd)",target=/home/jovyan/materials -it scipro jupyter lab --IdentityProvider.token=
# podman run --rm --name scipro -p 8888:8888 -p 9001:9001 --userns=keep-id -v "$(pwd):/home/jovyan/materials:Z" -it scipro jupyter lab --IdentityProvider.token=
## Open http://localhost:8888 in the browser
## If port 8888 is already allocated, try "-p 9999:8888" and open http://localhost:9999

# https://quay.io/repository/jupyter/base-notebook?tab=tags https://github.com/jupyter/docker-stacks/blob/main/images/base-notebook/Dockerfile
FROM quay.io/jupyter/base-notebook:lab-4.3.6 AS base_image

# https://github.com/moby/buildkit/blob/master/frontend/dockerfile/docs/reference.md#example-cache-apt-packages
USER root
RUN rm -f /etc/apt/apt.conf.d/docker-clean; echo 'Binary::apt::APT::Keep-Downloaded-Packages "true";' > /etc/apt/apt.conf.d/keep-cache
RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
  --mount=type=cache,target=/var/lib/apt,sharing=locked \
  apt-get update && apt-get install -yq --no-install-recommends \
    # memray's native mode resolves symbols using debuginfod, https://bloomberg.github.io/memray/native_mode.html#debuginfod-integration
    debuginfod && \
    # build dependencies for scalene https://pypi.org/project/scalene/#files
    if [ "$(dpkg --print-architecture)" != "amd64" ]; then apt-get install -yq --no-install-recommends build-essential; fi && \
  rm -rf $HOME/work
ENV DEBUGINFOD_URLS="https://debuginfod.ubuntu.com/"

# $NB_USER is jovyan
USER $NB_USER

# Execute all following RUN commands inside the conda "base" environment, https://pythonspeed.com/articles/activate-conda-dockerfile
SHELL ["conda", "run", "--no-capture-output", "-n", "base", "/bin/bash", "-c"]

# Try a fast pip alternative
RUN pip install uv==0.6.6

# Add python packages, https://stackoverflow.com/questions/58018300/using-a-pip-cache-directory-in-docker-builds
# Create cache directory to avoid root ownership
RUN mkdir -p $HOME/.cache
RUN --mount=type=cache,uid=$NB_UID,mode=7777,target=$HOME/.cache/uv \
  uv pip install \
    # jupyterlab is preinstalled in the base image
    # jupyterlab==4.3.6 \
    # alternative to jupyter notebooks
    marimo==0.11.20 \
    # start marimo notebooks from jupyterlab
    jupyter-marimo-proxy==0.0.4 \
    # try to automatically import missing imports
    jupyterlab-pyflyby==5.1.2 \
    pyflyby==1.9.11 \
    # visualization
    altair==5.5.0 \
    # visualization
    hvplot==0.11.2 \
    # visualization
    matplotlib==3.10.1 \
    # memary profiler (tracer)
    memray==1.16.0 \
    # just-in-time compiler for numerical functions
    numba==0.61.0 \
    # arrays, version set by numba
    numpy \
    # dataframes
    pandas==2.2.3 \
    # visualization
    plotly==6.0.0 \
    # dataframes
    polars==1.25.2 \
    # polars backend, only used for to_pandas() when plotting with hvplot
    pyarrow==19.0.1 \
    # CPU, GPU, and memory profiler (sampler)
    scalene==1.5.51 \
    # algorithms for scientific computing
    scipy==1.15.2 \
    # python tracer
    viztracer==1.0.3 && \
  # load pyflyby automatically
  py pyflyby.install_in_ipython_config_file

# Fix for jupyter-marimo-proxy
ENV JUPYTERHUB_SERVICE_PREFIX="/"

# RUN --mount=type=cache,uid=$NB_UID,mode=7777,target=$HOME/.conda/pkgs \
#   export CONDA_PKGS_DIRS=$HOME/.conda/pkgs && \
#   mamba install -y -c conda-forge \
#     git
