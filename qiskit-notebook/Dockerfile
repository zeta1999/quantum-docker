FROM jupyter/base-notebook

ARG qiskit_version
RUN test -n "$qiskit_version" || (echo "qiskit_version is not set" && false)

# Install Linux packages that are needed when we install the Qiskit
USER root
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
 && apt-get install -yq --no-install-recommends \
    gcc \
    libc6-dev \
 && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Qiskit with visualization
USER $NB_UID
RUN pip install 'qiskit[visualization]'==${qiskit_version}

# Copy default notebooks
COPY ./work /home/$NB_USER/work