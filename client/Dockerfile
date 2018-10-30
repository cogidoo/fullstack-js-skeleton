FROM node:latest 

RUN mkdir -p /opt/app

# default to port 4200
ARG PORT=4200
ENV PORT ${PORT}
EXPOSE ${PORT}

# place npm global dependencies into /opt
ENV NPM_CONFIG_PREFIX /opt/.npm-global
ENV PATH /opt/.npm-global/bin:$PATH

# you'll likely want the latest npm, reguardless of node version, for speed and fixes
RUN npm install -g npm@latest

# install angular cli
RUN npm install -g @angular/cli

# first install dependencies
WORKDIR /opt
COPY package.json package-lock.json* ./
RUN npm install && npm cache clean --force
ENV PATH /opt/node_modules/.bin:$PATH

# now copy source code as it changes the most
WORKDIR /opt/app
COPY . /opt/app
