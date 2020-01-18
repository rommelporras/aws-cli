FROM python:3.8-alpine

LABEL maintainer="Rommel Porras <devops@rommelporras.com>"
LABEL author="Rommel Porras"
LABEL version="1.16.305"
LABEL aws_build_date="Dec 18, 2019"

# Versions: https://pypi.python.org/pypi/awscli#downloads
ENV AWS_CLI_VERSION 1.16.305

RUN apk --no-cache update && \
    apk --no-cache add \
        ca-certificates \
        groff \
        less \
        && \
    pip3 --no-cache-dir install awscli==${AWS_CLI_VERSION} && \
    rm -rf /var/cache/*

WORKDIR /data

ENTRYPOINT ["aws"]