FROM debian:latest

ENV TS_VERSION=3.0.13.6
ENV LD_LIBRARY_PATH=/data

RUN apt-get update \
	&& apt-get install -y bzip2 wget \
	&& rm -rf /var/lib/apt/lists/* \
	&& apt-get autoremove \
    && useradd -M --uid 1000 teamspeak \
    && mkdir /data \
    && chown teamspeak:teamspeak /data

ADD http://dl.4players.de/ts/releases/3.0.13.6/teamspeak3-server_linux_amd64-${TS_VERSION}.tar.bz2 /data

COPY start_server.sh /start_server

RUN cd /data \
	&& tar -xvf teamspeak3-server_linux_amd64-${TS_VERSION}.tar.bz2 --strip-components=1 \
	&& rm -rf teamspeak3-server_linux_amd64-${TS_VERSION}.tar.bz2

EXPOSE 9987/udp 30033 10011

WORKDIR /data

USER teamspeak

CMD ["./ts3server", "createinifile=1"]