FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

FROM nginx:stable-alpine

RUN mkdir -p /etc/nginx/ssl

COPY --from=build /app/build /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY certs/ssl.crt /etc/nginx/ssl/ssl.crt
COPY certs/ssl.key /etc/nginx/ssl/ssl.key

EXPOSE 443
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]