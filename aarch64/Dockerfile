FROM arm64v8/node:lts-alpine

# Experimental ARMv8 support for Node-RED

# Home directory for Node-RED application source code.
# User data directory, contains flows, config and nodes.
# Add node-red user so we aren't running as root.
RUN mkdir -p /usr/src/node-red \
    && mkdir /data \
    && adduser -h /usr/src/node-red -H -D node-red node-red \
    && chown -R node-red:node-red /data \
    && chown -R node-red:node-red /usr/src/node-red

WORKDIR /usr/src/node-red

USER node-red

# package.json contains Node-RED NPM module and node dependencies
COPY package.json /usr/src/node-red/
RUN npm install

# User configuration directory volume
VOLUME [ "/data" ]

# Exposing port
EXPOSE 1880

# Environment variable holding file path for flows configuration
ENV FLOWS=flows.json

CMD ["npm", "start", "--", "--userDir", "/data"]
