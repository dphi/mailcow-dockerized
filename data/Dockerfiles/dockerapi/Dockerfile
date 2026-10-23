FROM alpine:3.21.9@sha256:ee16d92f96db08d9d2d07da48555a27f3a69d8f0759021dbc601195ed0d2b5bd

LABEL maintainer = "The Infrastructure Company GmbH <info@servercow.de>"

ARG PIP_BREAK_SYSTEM_PACKAGES=1
WORKDIR /app

RUN apk add --update --no-cache python3 \
  py3-pip \
  openssl \
  tzdata \
  py3-psutil \
  py3-redis \
  py3-async-timeout \
&& pip3 install --upgrade pip \
  fastapi \
  uvicorn \
  aiodocker \
  docker
RUN mkdir /app/modules

COPY docker-entrypoint.sh /app/
COPY main.py /app/main.py
COPY modules/ /app/modules/

ENTRYPOINT ["/bin/sh", "/app/docker-entrypoint.sh"]
CMD ["python", "main.py"]