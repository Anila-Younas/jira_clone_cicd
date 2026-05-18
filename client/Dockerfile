# Stage 1: Build the React app
FROM mcr.microsoft.com/devcontainers/javascript-node:18-bullseye AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .

# THIS IS THE FIX: Tell Node 18 to allow legacy React build tools
ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]