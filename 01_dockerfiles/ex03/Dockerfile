FROM debian

RUN apt-get update -y \
	&& apt-get install -y git wget gcc \
	&& apt-get autoremove

WORKDIR /local
RUN wget https://storage.googleapis.com/golang/go1.8.linux-amd64.tar.gz
RUN tar -xzvf go1.8.linux-amd64.tar.gz

ENV GOROOT=/local/go
ENV GOPATH=/gogs
ENV PATH=$PATH:$GOROOT/bin:$GOPATH/bin

WORKDIR $GOPATH/src/github.com/gogits

RUN git clone --depth=1 -b develop https://github.com/gogits/gogs
RUN go get -u -tags "sqlite" github.com/gogits/gogs

WORKDIR $GOPATH/src/github.com/gogits/gogs
RUN go build -tags "sqlite"

RUN mkdir $GOPATH/src/github.com/gogits/logs
RUN mkdir /root/gogs-repositories
RUN mkdir /root/data
RUN mkdir -p /gogs/src/github.com/gogits/gogs/custom/conf
RUN echo \
	"RUN_USER = root \n\
	\n\
	[repositories] \n\
	ROOT = "/root/gogs-repositories" \n\
	\n\
	[server] \n\
	DOMAIN = 192.168.99.100 \n\
	ROOT_URL = %(PROTOCOL)s://%(DOMAIN)s:8300/ \n\
	SSH_PORT = 8322 \n\
	SSH_ROOT_PATH = '/home/git/.ssh' \n\
 	\n\
	[database] \n\
	DB_TYPE = sqlite3 \n\
	PATH = /root/data/gogs.db \n\
	 \n\
	[security] \n\
	INSTALL_LOCK = true \
	" > /gogs/src/github.com/gogits/gogs/custom/conf/app.ini

EXPOSE 3000 22

ENV USER=root

CMD ./gogs web