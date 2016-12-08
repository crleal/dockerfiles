# Base docker image
FROM ubuntu:latest
MAINTAINER Clementino Leal <crl.leal@gmail.com>
 
RUN         apt-get update && apt-get install -y redis-server
EXPOSE      6379
ENTRYPOINT  ["/usr/bin/redis-server"]

