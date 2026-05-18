# Stage 1: Build the React app
FROM mcr.microsoft.com/devcontainers/javascript-node:18-bullseye AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Stage 2: Serve with Nginx
# Using the stable Docker Hub path - Azure agents can usually pull this 
# if the Node image is already pulled from MCR
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]