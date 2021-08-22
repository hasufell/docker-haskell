FROM debian:buster AS builder

ENV LANG C.UTF-8

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

ARG GHCUP_VERSION=0.1.16.2

RUN curl -fSL https://downloads.haskell.org/~ghcup/$GHCUP_VERSION/x86_64-linux-ghcup-$GHCUP_VERSION -o ghcup && \
    chmod +x ghcup

ARG CABAL_VERSION=3.4.0.0

RUN ./ghcup install cabal $CABAL_VERSION && \
    ./ghcup set cabal $CABAL_VERSION

ARG GHC_VERSION=8.10.6

RUN ./ghcup install ghc $GHC_VERSION && \
    ./ghcup set ghc $GHC_VERSION

ARG STACK_VERSION=2.7.3

RUN ./ghcup install stack $STACK_VERSION && \
    ./ghcup set stack $STACK_VERSION

RUN cp -H /root/.ghcup/bin/* /usr/local/bin