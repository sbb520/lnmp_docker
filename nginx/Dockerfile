FROM nginx
#COPY nginx.conf /etc/nginx/nginx.conf

RUN useradd www
RUN usermod -u 1000 www

WORKDIR /etc/nginx/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
