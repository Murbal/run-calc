# Client
FROM node:16-slim as client

WORKDIR /code
COPY docker/install-pnpm docker/pnpm-v6.16.js /scripts/
RUN ../scripts/install-pnpm

COPY client/package.json client/pnpm-lock.yaml /code/
RUN pnpm install

COPY client /code/
RUN pnpm build

# Nginx
FROM nginx

COPY docker/web/default.conf /etc/nginx/conf.d/default.conf
COPY --from=client /code/dist /usr/share/nginx/html