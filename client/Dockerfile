# Step 1: Build app using Node
FROM node:18-alpine AS build
WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm ci

# Copy rest of code and build
COPY . .
RUN npm run build

# Step 2: Serve using nginx
FROM nginx:stable-alpine
RUN rm -rf /usr/share/nginx/html/*

# Copy Vite build output (dist folder)
COPY --from=build /app/dist /usr/share/nginx/html

# If you have a custom nginx.conf file, enable the line below:
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]