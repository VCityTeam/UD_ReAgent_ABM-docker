FROM ubuntu:focal

LABEL maintainer "VCityTeam"
LABEL source.repo "https://github.com/VCityTeam/UD_ReAgent_ABM-docker"

RUN apt-get update

######### Install the UD-Viz demo per se (client code) and build it
# Node version 14 is required. For its installation (on focal) refer to e.g.
#  https://computingforgeeks.com/install-node-js-14-on-ubuntu-debian-linux/
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash -
RUN apt-get install -y nodejs
RUN node --version
RUN npm --version
RUN apt-get install -y git
RUN git --version


ARG checkoutName=master
RUN git clone https://github.com/VCityTeam/UD_ReAgent_ABM.git




######### Builds the application
WORKDIR /UD_ReAgent_ABM/UD-Viz-GCCV
RUN git checkout $checkoutName
RUN npm install
RUN npm run build




######### Install SimpleServer (an ExpressJS based...simple server)
WORKDIR /
RUN git clone https://github.com/VCityTeam/UD-SimpleServer
WORKDIR UD-SimpleServer
RUN npm install
CMD [ "node", "./index.js", "../UD_ReAgent_ABM/UD-Viz-GCCV", "8000" ]
