# Stage 1: Build frontend
FROM node:20-alpine AS build

# Set working directory
WORKDIR /app

# Copy package files first (for caching)
COPY package.json bower.json ./

# Install npm dependencies
RUN npm install --silent

# Install bower globally
RUN npm install -g bower --silent

# Copy all frontend source files required for build
COPY app/ ./app
COPY static-mock.js ./
COPY scripts/ ./scripts
COPY webpack.*.js ./
COPY vendor/ ./vendor

# Install bower dependencies
RUN bower install --allow-root

# Build frontend (adjust command if needed)
RUN npm run build

# Stage 2: Serve frontend with nginx
FROM nginx:alpine

# Remove default nginx content
RUN rm -rf /usr/share/nginx/html/*

# Copy built frontend
COPY --from=build /app/public /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
