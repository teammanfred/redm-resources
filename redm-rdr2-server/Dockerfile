FROM ubuntu:20.04
RUN apt update && DEBIAN_FRONTEND=noninteractive apt install -y curl git libxml2-utils xz-utils
WORKDIR /opt/redm
COPY setup /opt/redm/setup
RUN /opt/redm/setup
