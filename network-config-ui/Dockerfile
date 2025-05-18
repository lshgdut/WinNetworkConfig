FROM node:22-alpine AS builder
WORKDIR /work
COPY . .
RUN rm -rf dist && \
    npm config set registry "https://registry.npmmirror.com/" && \
    npm install && \
    npm run build

# 基础镜像声明
## 使用 scratch 作为基础镜像创建一个最小化的容器环境
FROM scratch

COPY --from=builder /work/dist /app

# 容器不运行任何主进程，仅作为卷容器使用
CMD [ "true" ]