FROM node:22-alpine AS builder
WORKDIR /work

ARG USE_CN_MIRROR

COPY . .
RUN \
    # If you want to build docker in China, build with --build-arg USE_CN_MIRROR=true
    if [ "${USE_CN_MIRROR:-false}" = "true" ]; then \
        npm config set registry "https://registry.npmmirror.com/"; \
    fi \
    && npm install \
    && npm run build

# 基础镜像声明
FROM nginx:1.28-alpine

ENV PORT=80
ENV NW_API_PORT=8080
COPY ./nginx.conf /etc/nginx/templates/default.conf.template
COPY --from=builder /work/dist /usr/share/nginx/html

# Switch to non-root user
# USER nginx

# Expose port
# EXPOSE 80

# Start Nginx
# CMD ["nginx", "-g", "daemon off;"]