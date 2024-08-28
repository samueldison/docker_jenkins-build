ARG VERSION=1.25

# choose a light weight base image
FROM nginx:${VERSION}-alpine-slim

ENV WORK_DIR=/usr/share/nginx/html

# working directory
WORKDIR ${WORK_DIR}

# copy all necessary web content with a single command
COPY healet-html/ ${WORK_DIR}

# expose static web site on a specific port
EXPOSE 80

# Add a health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 CMD curl -f http://localhost/index.html || exit 1

CMD ["nginx","-g","daemon off;"]
