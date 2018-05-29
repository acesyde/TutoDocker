# IMAGE DE BASE NODEJS EN VERSION LTS
FROM node:8-alpine as builder
# REPERTOIRE DE TRAVAIL
WORKDIR /src
# COPIE LES FICHIERS LOCAUX DANS L'IMAGE
COPY . /src
# INSTALL YARN
RUN yarn install
# COMPILE
RUN ["yarn","next","build"]
# GENERATION STATIC
RUN ["yarn","next","export"]

# WEB SERVER
FROM nginx:alpine
# COPIE LES FICHIERS GENERES VERS LE SITE NGINX
COPY --from=builder /src/out /usr/share/nginx/html

# forward nginx logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log