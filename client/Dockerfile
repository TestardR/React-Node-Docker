# Production
FROM node:10-alpine as builder

WORKDIR /client
COPY package*.json /client/

RUN npm install --only=prod

COPY . /client

# Build the production build
RUN npm run build

# Start and nginx container
FROM nginx:1.16.0-alpine

COPY --from=builder /client/build /usr/share/nginx/html

RUN rm /etc/nginx/conf.d/default.conf
COPY nginx/nginx.conf /etc/nginx/conf.d

COPY --from=builder /client/build /usr/share/nginx/html
RUN chown nginx.nginx /usr/share/nginx/html/ -R

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]