FROM node:5

# sources.list.jessie is downloaded from http://mirrors.163.com/.help/debian.html
COPY sources.list.jessie /etc/apt/sources.list

RUN apt-get -y update \
    && apt-get -y install sudo

# Comment the next line If you are not in china
RUN npm config set registry https://registry.npm.taobao.org \
   && npm install -g yo \
   && npm install -g generator-fountain-webapp \
   && npm install -g generator-react-webpack \
   && npm install -g gulp-cli

# Add a yeoman user because grunt doesn't like being root
RUN adduser --disabled-password --gecos "" yeoman && \
 echo "yeoman ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# set HOME so 'npm install' and 'bower install' don't write to /
ENV HOME /home/yeoman

RUN mkdir /usr/src/app && chown yeoman:yeoman /usr/src/app
WORKDIR /usr/src/app

# Always run as the yeoman user
USER yeoman

# reference: https://github.com/npm/npm/issues/7308
RUN echo "alias npm='npm --no-bin-links'" >> /home/yeoman/.bash_aliases \
    && source /home/yeoman/.bash_aliases

RUN npm config set registry https://registry.npm.taobao.org

#CMD /bin/bash
