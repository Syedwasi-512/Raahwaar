# ================================
# Stage 1 — Builder
# ================================

FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json .
RUN npm install --legacy-peer-deps
COPY . .

# ================================
# Stage 2 — Runner
# ================================

FROM node:20-alpine AS runner
WORKDIR /app

# Sirf production dependencies
COPY package*.json .
RUN npm install --only=production --legacy-peer-deps

COPY . .
EXPOSE 5000
CMD ["node", "server.js"]

