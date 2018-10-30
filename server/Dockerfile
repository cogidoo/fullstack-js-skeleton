FROM node:latest 

RUN mkdir -p /opt/app

# set node environment - either development or production
# defaults to production, but docker-compose overrides this to development on build and run
ARG NODE_ENV=production
ENV NODE_ENV ${NODE_ENV}

# default to port 80 for node, and 9229 and 9230 (tests) for debug
ARG PORT=80
ENV PORT ${PORT}
EXPOSE ${PORT} 9229 9230

# place npm global dependencies into /opt
ENV NPM_CONFIG_PREFIX /opt/.npm-global
ENV PATH /opt/.npm-global/bin:$PATH

# you'll likely want the latest npm, reguardless of node version, for speed and fixes
RUN npm install -g npm@latest

# first install dependencies - in an extra directory for better local-development-mounting
WORKDIR /opt
COPY package.json package-lock.json* ./
RUN npm install && npm cache clean --force
ENV PATH /opt/node_modules/.bin:$PATH

# check every 30s to ensure this service returns HTTP 200
HEALTHCHECK --interval=30s CMD node healthcheck.js

# now copy source code as it changes the most
WORKDIR /opt/app
COPY . /opt/app

CMD [ "node", "index.js" ]