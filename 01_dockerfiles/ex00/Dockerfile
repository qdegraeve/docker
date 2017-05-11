FROM alpine:latest

WORKDIR /app

ADD . /app

RUN apk update && apk add vim

ENTRYPOINT ["vim"]
