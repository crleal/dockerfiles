# Base docker image
FROM ubuntu:latest
MAINTAINER Clementino Leal <crl.leal@gmail.com>
 
RUN useradd developer && \
        apt-get update && \
 	apt-get install -qqy x11-apps firefox wget libcurl3 libnss3-tools ; \
 	apt-get clean 

# plugin para itau funcionar no firefox docker, caso não precise pode comentar 
RUN cd /tmp  &&  \
    wget https://guardiao.itau.com.br/warsaw/warsaw_setup_64.deb &&  \
    dpkg -i warsaw_setup_64.deb 
 
USER developer

ENV HOME /home/developer
 
CMD ["/usr/lib/firefox/firefox", "--no-remote"]


# The --no-remote option forces firefox to open a new window from within the container, 
# instead of just opening a new window from your already running firefox on the host system.

