FROM node:16.13.0-alpine as builder

RUN mkdir -p /home/app
WORKDIR '/app'
COPY --chown=node:node package.json .
RUN npm install
COPY --chown=node:node . .
RUN npm run build

FROM nginx:alpine
EXPOSE 3000
COPY --chown=node:node ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --chown=node:node --from=builder /app/build /usr/share/nginx/html