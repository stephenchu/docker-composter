FROM vault:latest

WORKDIR /root

RUN apk update \
  &&  apk add --no-cache \
    bash \
    vim \
    jq \
    curl

RUN \
  curl -fsSL https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh -o /usr/local/bin/wait-for-it.sh \
    && chmod +x /usr/local/bin/wait-for-it.sh

COPY \
  configure/scripts/start \
  configure/scripts/init-and-unseal ./

CMD \
  ( wait-for-it.sh --host=127.0.0.1 --port=8200 --strict -- ./init-and-unseal ) & \
  ./start
