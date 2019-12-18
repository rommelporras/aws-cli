FROM python:3.8-alpine

# Versions: https://pypi.python.org/pypi/awscli#downloads
# v1.16.305 Build date Dec 18, 2019
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