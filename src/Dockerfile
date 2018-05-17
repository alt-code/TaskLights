FROM ubuntu:16.04

RUN apt-get update
RUN apt-get -y install git vim python-minimal python-pip
RUN apt-get -y install build-essential libssl-dev

RUN apt-get -y install libudev-dev libusb-1.0-0-dev libfox-1.6-dev

RUN apt-get -y install libasound2-dev


RUN apt-get -y install curl
RUN curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install -y nodejs
RUN node -v

RUN apt-get install -y usbutils
#RUN apt-get -y install alsa-utils

ADD . /TaskLights
# Remove any old builds that might be copied over.
RUN rm -rf /TaskLights/node_modules
RUN cd /TaskLights && npm install 
