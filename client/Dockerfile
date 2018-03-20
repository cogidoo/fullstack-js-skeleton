FROM node:carbon 

RUN mkdir -p /opt/app

# set node environment - either development or production
# defaults to production, but docker-compose overrides this to development on build and run
ARG NODE_ENV=production
ENV NODE_ENV ${NODE_ENV}

# place npm global dependencies into /opt
ENV NPM_CONFIG_PREFIX /opt/.npm-global
ENV PATH /opt/.npm-global/bin:$PATH

# first install dependencies
WORKDIR /opt
COPY package.json package-lock.json* ./
RUN npm install && npm cache clean --force
ENV PATH /opt/node_modules/.bin:$PATH

# now copy source code as it changes the most
WORKDIR /opt/app
COPY . /opt/app