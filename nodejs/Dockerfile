ARG MAINTAINER
FROM debian:stable-slim
MAINTAINER $MAINTAINER

ARG NODE_VERSION=16

# Install Packages (basic and NodeJS development tools from upstream repository)
RUN apt-get update \
&& apt-get install -y curl gnupg \
&& curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -\
&& echo "deb http://deb.nodesource.com/node_${NODE_VERSION}.x bullseye main" \
  > /etc/apt/sources.list.d/nodejs.list \
&& apt-get update \
&& apt-get install -y sudo git nodejs \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

# Add node user and disable sudo password checking
RUN useradd \
  --groups=sudo \
  --create-home \
  --home-dir=/home/node \
  --shell=/bin/bash \
  node \
&& sed -i '/%sudo[[:space:]]/ s/ALL[[:space:]]*$/NOPASSWD:ALL/' /etc/sudoers

# Setup environment
USER node
WORKDIR /home/node

# Default shell
CMD ["/bin/bash","--login","-i"]
