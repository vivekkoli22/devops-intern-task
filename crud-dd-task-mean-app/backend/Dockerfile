# backend/Dockerfile
FROM node:18-alpine

WORKDIR /usr/src/app

# copy package files first for caching
COPY package*.json ./

# install dependencies (if package-lock.json exists npm ci, else npm install)
RUN npm ci --only=production || npm install

# copy source code
COPY . .

# set node environment (optional)
ENV NODE_ENV=production
ENV PORT=3000

EXPOSE 3000

# start the server - uses server.js present in your backend folder
CMD ["node", "server.js"]
