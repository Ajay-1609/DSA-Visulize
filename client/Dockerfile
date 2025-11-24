# Build Stage
FROM node:18 AS build
WORKDIR /app

COPY package*.json ./
COPY . .

RUN npm install
RUN npm run build

# Production Stage
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html

# Replace default nginx config to enable client routing (SPA support)
RUN printf "server {\n\
  listen 80;\n\
  server_name localhost;\n\
  root /usr/share/nginx/html;\n\
  location / {\n\
    try_files \$uri /index.html;\n\
  }\n\
}" > /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]