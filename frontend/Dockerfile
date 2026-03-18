FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json .

RUN npm install --legacy-peer-deps

COPY . . 

ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL

RUN npm run build

# Ab /app/dist mein final files hain ✅

# ================================
# Stage 2 — Runner (Sirf nginx!)
# ================================

FROM nginx:alpine AS runner

# Builder se sirf dist folder lo
COPY --from=builder /app/dist /usr/share/nginx/html

# nginx config copy karo
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]