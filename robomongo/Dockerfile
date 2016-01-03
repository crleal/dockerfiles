FROM ubuntu:latest

RUN apt-get update && apt-get install -yq curl

# install dependencies...
RUN apt-get update && apt-get install -yq \
	libglib2.0-0 \
	libgl1-mesa-glx libgl1-mesa-dri \
	libqt5gui5

RUN \
	curl -L http://app.robomongo.org/files/linux/robomongo-0.8.5-x86_64.deb > /usr/src/robomongo.deb && \
      dpkg --force-depends -i /usr/src/robomongo.deb && \
	apt-get install -fy \
	&& rm -rf /var/lib/apt/lists/*
	

CMD [ "robomongo" ]
