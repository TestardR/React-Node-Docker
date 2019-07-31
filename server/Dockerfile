# Production
FROM node:10-alpine as builder 

WORKDIR /server

COPY package*.json /server/

RUN npm install --only=prod

COPY . /server/

FROM node:10-alpine 

WORKDIR /server

COPY --from=builder /server /server

CMD ["node", "server.js"]