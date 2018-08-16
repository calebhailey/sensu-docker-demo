# Source
FROM debian:stretch

# Labels
LABEL vendor=Sensu,\ Inc. \
  io.sensu.version="1.4.2" \
  io.sensu.release-date="2018-07-08"

# Build arguments
ARG SENSU_REPO_HOST=https://repositories.sensuapp.org
ARG SENSU_REPO_PATH=/apt/pool/stretch/main/s/sensu/
ARG SENSU_PACKAGE_FILENAME=sensu_1.4.2-4_amd64.deb

# Environment Variables
ENV \
  SENSU_LOG_LEVEL="info" \
  SENSU_CLIENT_SUBSCRIPTIONS="all,docker" \
  SENSU_TRANSPORT_NAME="redis" \
  REDIS_URL="redis://${SENSU_REDIS_SERVICE_HOST:-127.0.0.1}:${SENSU_REDIS_SERVICE_PORT:-6379}"

# Build instructions
WORKDIR /build
RUN \
  apt-get update && \
  apt-get install -y curl && \
  echo "Downloading installer package: ${SENSU_REPO_HOST}/${SENSU_REPO_PATH}/${SENSU_PACKAGE_FILENAME}" && \
  curl -L -O ${SENSU_REPO_HOST}/${SENSU_REPO_PATH}/${SENSU_PACKAGE_FILENAME} && \
  dpkg -i ${SENSU_PACKAGE_FILENAME} && \
  rm -f ${SENSU_PACKAGE_FILENAME} && \
  echo "EMBEDDED_RUBY=true" | tee /etc/default/sensu && \
  /opt/sensu/bin/sensu-client --print_config -d /etc/sensu/conf.d/

CMD ["/opt/sensu/bin/sensu-client"]
