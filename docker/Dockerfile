FROM node:18-bullseye
WORKDIR /usr/src/app
COPY package.json package-lock.json* ./ 
RUN npm install --unsafe-perm
COPY . .
EXPOSE 3000
CMD ["bash", "-lc", "npm run webpack -- --watch & npm run proxy"]
