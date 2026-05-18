# Stage 1: Build
FROM mcr.microsoft.com/devcontainers/javascript-node:18-bullseye AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Stage 2: Production
FROM mcr.microsoft.com/devcontainers/javascript-node:18-bullseye
WORKDIR /app
# Changed /app/dist to /app/build to match jira_clone output
COPY --from=builder /app/build ./build
COPY --from=builder /app/node_modules ./node_modules
COPY package*.json ./

EXPOSE 3000
# Updated CMD to point to the build folder
CMD ["node", "build/index.js"]