##choose a light weight base image
FROM nginx:1.25-alpine-slim

# working directory
WORKDIR /usr/share/nginx/html

# copy web contents into static html dir
COPY . /usr/share/nginx/html

# remove Dockerfile that was copied into the static web dir
RUN rm -rf D*

# expose static web app on a specific port
EXPOSE 80

CMD ["nginx","-g","daemon off;"]

