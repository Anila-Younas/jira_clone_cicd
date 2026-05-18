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
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY package*.json ./

EXPOSE 3000
CMD ["node", "dist/index.js"]