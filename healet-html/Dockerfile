# syntax=docker/dockerfile:1

ARG VERSION=1.25

# Stage 1: Build stage with necessary dependencies
FROM nginx:${VERSION}-alpine-slim AS build
 
ENV WORK_DIR=/usr/share/nginx/html

# Create a working directory in the image
WORKDIR ${WORK_DIR}

# Copy all web contents from host to image
COPY . ${WORK_DIR}

# Stage 2: Final stage with minimal footprint
FROM nginx:${VERSION}-alpine-slim AS final

ENV WORK_DIR=/usr/share/nginx/html

# Copy built artifacts from the build stage to the final stage
COPY --from=build ${WORK_DIR} ${WORK_DIR}

# Install curl for health check in final stage
RUN apk add --no-cache curl

# Expose static web app on port 80
EXPOSE 80

# Add a health check to monitor the app
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 CMD curl -f http://localhost/index.html || exit 1

# Run Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
