FROM ubuntu:jammy-20230308

ARG RUNNER_BASE_VERSION=2.303.0

RUN apt-get update -q \
    && apt-get install -y --no-install-recommends \ 
			curl=7.81.0-1ubuntu1.8 \
			ca-certificates=20211016ubuntu0.22.04.1 \
		git=1:2.34.1-1ubuntu1.8 \
		&& apt-get autoremove -y \
		&& apt-get clean -y \
		&& rm -rf /var/lib/apt/lists/* \
			/root/.gnupg \
			/tmp/library-scripts

RUN adduser --shell /bin/bash --home /home/runner --disabled-password --gecos "" runner

WORKDIR /home/runner

RUN git clone https://github.com/asdf-community/asdf-ubuntu.git \
	&& cp asdf-ubuntu/asdf-install-toolset /usr/local/bin \
	&& rm -rf asdf-ubuntu

USER runner
RUN git clone --depth 1 "https://github.com/asdf-vm/asdf.git" "$HOME/.asdf" && \
    echo ". $HOME/.asdf/asdf.sh" >> "$HOME/.bashrc" && \
    echo ". $HOME/.asdf/asdf.sh" >> "$HOME/.profile"

WORKDIR /runner
RUN chown runner: /runner

RUN curl -o actions-runner-linux-x64.tar.gz  -L "https://github.com/actions/runner/releases/download/v${RUNNER_BASE_VERSION}/actions-runner-linux-x64-${RUNNER_BASE_VERSION}.tar.gz" \
    && tar xzf actions-runner-linux-x64.tar.gz \
    && rm actions-runner-linux-x64.tar.gz

USER root
RUN ./bin/installdependencies.sh \
	&& apt-get autoremove -y \
	&& apt-get clean -y \
	&& rm -rf /var/lib/apt/lists/* \
	/root/.gnupg /tmp/library-scripts

USER runner

ENTRYPOINT ["/run.sh"]
