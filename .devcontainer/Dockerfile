# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.187.0/containers/python-3/.devcontainer/base.Dockerfile

# [Choice] Python version: 3, 3.9, 3.8, 3.7, 3.6
ARG VARIANT="3.10"
FROM mcr.microsoft.com/devcontainers/python:${VARIANT}

RUN \
    apt-get upgrade \
    && apt-get update \
    && apt-get install -y bash-completion curl openjdk-17-jdk \
    && pip install pre-commit

# Install Kafka CLI tools
RUN cd /tmp && \
    KAFKA_VERSION="3.9.0" && \
    SCALA_VERSION="2.13" && \
    wget "https://downloads.apache.org/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz" && \
    tar -xzf "kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz" -C /opt/ && \
    mv "/opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}" /opt/kafka && \
    rm "kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz" && \
    chown -R vscode:vscode /opt/kafka

ENV PATH="${PATH}:/opt/kafka/bin"

# Coding only for vscode user and not root
USER vscode

RUN curl -sSL https://install.python-poetry.org | python3 - \
    && bash -c "echo 'source <(poetry completions bash)' >> ~/.bashrc"
