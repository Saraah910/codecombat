FROM node:20-alpine

WORKDIR /app

# Copy package files
COPY package.json package-lock.json ./
RUN npm ci --silent

# Copy backend source code (CodeCombat uses server.js and many folders)
COPY server.js ./
COPY server_config.js ./
COPY server_setup.js ./
COPY nodemon.json ./
COPY development ./development
COPY patches ./patches
COPY ozaria ./ozaria
COPY app ./app
COPY vendor ./vendor
COPY scripts ./scripts
COPY server_config.js ./
COPY static-mock.js ./
COPY webpack.*.config.js ./

# Copy .env file (optional; can be mounted instead)
COPY .env /app/.env

# Install additional OS deps (if needed)
RUN apk add --no-cache bash

EXPOSE 3000

CMD ["node", "server.js"]
