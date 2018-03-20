FROM node:carbon 

RUN mkdir -p /opt/app

# set node environment - either development or production
# defaults to production, but docker-compose overrides this to development on build and run
ARG NODE_ENV=production
ENV NODE_ENV ${NODE_ENV}

# place npm global dependencies into /opt
ENV NPM_CONFIG_PREFIX /opt/.npm-global
ENV PATH /opt/.npm-global/bin:$PATH

# default to port 80 for node, and 5858/9229 for debug
ARG PORT=80
ENV PORT ${PORT}
EXPOSE ${PORT} 5858 9229

# check every 30s to ensure service return HTTP 200
HEALTHCHECK CMD curl -fs http://localhost:${PORT}/healthz || exit 1

WORKDIR /opt/app

# first install dependencies
COPY package.json package-lock.json* ./
RUN npm install && npm cache clean --force
ENV PATH /opt/app/node_modules/.bin:$PATH

# now copy source code as it changes the most
COPY . /opt/app

CMD [ "node", "index.js" ]