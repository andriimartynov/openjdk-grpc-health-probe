FROM openjdk:11-jre-slim
LABEL maintainer="Andrii Martynov andrii.martynov@gmail.com"

RUN savedAptMark="$(apt-mark showmanual)"; \
    apt-get update; \
	apt-get install -y --no-install-recommends \
		wget

# Install grpc-health-probe
RUN mkdir /opt/docker &&\
    mkdir /opt/docker/bin &&\
    wget -qO/opt/docker/bin/grpc_health_probe \
    https://github.com/grpc-ecosystem/grpc-health-probe/releases/download/v0.3.0/grpc_health_probe-linux-amd64; \
    chmod +x /opt/docker/bin/grpc_health_probe

RUN apt-mark auto '.*' > /dev/null; \
    [ -z "$savedAptMark" ] || apt-mark manual $savedAptMark > /dev/null; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \