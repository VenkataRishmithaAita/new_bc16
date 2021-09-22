FROM node:10-alpine as baseimage

COPY ["package.json","/."]
RUN npm install 
RUN mkdir /app 
RUN mv ./node_modules ./app    
WORKDIR /app 
COPY . . 
EXPOSE 8080
RUN npm run build-prod



FROM nginx:alpine
COPY --from=baseimage /app/dist /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

CMD ["nginx", "-g", "daemon off;"]
