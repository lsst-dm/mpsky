FROM condaforge/miniforge3

RUN mamba install -c conda-forge pytables tqdm pyarrow healpy pydantic-settings astropy pandas requests uvicorn fastapi zstandard
RUN apt-get update && apt-get install -y bc curl && apt-get clean && rm -rf /var/lib/apt/lists/*

# install mpsky from source
WORKDIR /app

COPY . /app/

RUN python -m pip install -e .
RUN mpsky --help

# Usual entrypoint. Best to run with
# docker run -it --rm --tmpfs /tmp:size=100m -p 8000:8000 --read-only mpsky-daily --host 0.0.0.0 --verbose
COPY docker/entrypoint.sh /entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

# switch to non-privileged user
USER ubuntu
ENV MPLCONFIGDIR=/tmp
