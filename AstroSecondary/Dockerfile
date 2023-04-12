FROM node:18-alpine as build

WORKDIR /app

COPY package.json package.json
COPY tsconfig.json tsconfig.json
COPY astro.config.mjs astro.config.mjs
COPY src ./src
COPY public ./public

RUN npm install
RUN npm run build

FROM nginx:alpine
COPY /nginx.conf /etc/nginx/nginx.conf
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=build app/dist .
EXPOSE 8080
ENTRYPOINT ["nginx", "-g", "daemon off;"]