# AgentStack 50 站点部署工件
# 镜像内零构建：nginx:alpine 直接伺服仓库根的静态文件
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
HEALTHCHECK --interval=30s --timeout=3s CMD wget -qO- http://127.0.0.1/ >/dev/null || exit 1
