# frontend/Dockerfile
FROM node:18-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm ci || npm install
COPY . .
# Angular production build (if CLI config different, this still usually works)
RUN npm run build -- --output-path=dist --configuration production

# Serve with nginx
FROM nginx:stable-alpine
# If Angular outputs to dist/<projectname>, copy that folder. If output is dist only, use that.
COPY --from=build /app/dist /usr/share/nginx/html

# replace default config with our SPA config
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
