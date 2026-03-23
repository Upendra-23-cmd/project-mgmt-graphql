FROM node:16-buster as builder

WORKDIR /app

COPY package.json /app/package.json
COPY package-lock.json /app/package-lock.json

RUN npm ci

RUN mkdir node_modules/.cache && chmod -R 777 node_modules/.cache

COPY . /app

RUN npm run build

FROM nginx:alpine

COPY --from=builder /app/build/ /usr/share/nginx/html

EXPOSE  80

CMD [ "nginx", "-g", "daemon off;" ]