FROM debian:bullseye-slim

ARG RUNNER_BASE_VERSION=2.303.0

WORKDIR /runner

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl=7.74.0-1.3+deb11u7 ca-certificates=20210119 \
    && rm -rf /var/lib/apt/lists/*

RUN curl -o actions-runner-linux-x64.tar.gz  -L "https://github.com/actions/runner/releases/download/v${RUNNER_BASE_VERSION}/actions-runner-linux-x64-${RUNNER_BASE_VERSION}.tar.gz" \
    && tar xzf actions-runner-linux-x64.tar.gz \
    && rm actions-runner-linux-x64.tar.gz
