FROM node:14.8-alpine as build
WORKDIR /app
COPY package*.json ./
RUN npm install --silent
COPY . /app
RUN npm run build

# production
FROM nginx:1.19.1-alpine as production-stage
COPY --from=build /app/dist /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY docker/nginx/nginx.conf /etc/nginx/conf.d
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]