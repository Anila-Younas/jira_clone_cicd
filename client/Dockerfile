# Stage 1: Build the React app
FROM mcr.microsoft.com/devcontainers/javascript-node:18-bullseye AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .

# --- THE FIX: Inject the Backend URL directly into the build environment ---
ENV API_URL=https://app-jiracicd-backend-anila-drhdh3cde9badvcc.eastasia-01.azurewebsites.net
ENV REACT_APP_API_URL=https://app-jiracicd-backend-anila-drhdh3cde9badvcc.eastasia-01.azurewebsites.net
ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]