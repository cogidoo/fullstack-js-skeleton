FROM node:carbon 

RUN mkdir -p /opt/app

# set node environment - either development or production
# defaults to production, but docker-compose overrides this to development on build and run
ARG NODE_ENV=production
ENV NODE_ENV ${NODE_ENV}

# place npm global dependencies into /opt
ENV NPM_CONFIG_PREFIX /opt/.npm-global
ENV PATH /opt/.npm-global/bin:$PATH

WORKDIR /opt/app

WORKDIR /opt/app

# first install dependencies
COPY package.json package-lock.json* ./
RUN npm install && npm cache clean --force
ENV PATH /opt/app/node_modules/.bin:$PATH

# now copy source code as it changes the most
COPY . /opt/app