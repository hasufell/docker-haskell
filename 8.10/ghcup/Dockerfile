FROM debian:buster AS builder

ENV LANG C.UTF-8

# install prerequisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        build-essential \
        libffi-dev \
        libffi6 \
        libgmp-dev \
        libgmp10 \
        libncurses-dev \
        libncurses5 \
        libtinfo5 \
        curl && \
    rm -rf /var/lib/apt/lists/*

# install ghcup
ARG GHCUP_VERSION=0.1.16.2
RUN curl --proto '=https' --tlsv1.2 -sSf https://downloads.haskell.org/~ghcup/$GHCUP_VERSION/x86_64-linux-ghcup-$GHCUP_VERSION > /usr/bin/ghcup && \
    chmod +x /usr/bin/ghcup

# install cabal
ARG CABAL_VERSION=3.4.0.0
RUN ghcup install cabal -i /usr/bin $CABAL_VERSION

# install stack
ARG STACK_VERSION=2.7.3
RUN ghcup install stack -i /usr/bin $STACK_VERSION

# install GHC into /opt/ghc
ARG GHC_VERSION=8.10.6
RUN ghcup install ghc -i /opt/ghc $GHC_VERSION

# Adjust PATH
RUN echo 'export PATH="/opt/ghc/bin:$PATH"' >> /etc/profile.d/ghcup_path.sh && \
	chmod +x /etc/profile.d/ghcup_path.sh
ENV PATH="/opt/ghc/bin:$PATH"
