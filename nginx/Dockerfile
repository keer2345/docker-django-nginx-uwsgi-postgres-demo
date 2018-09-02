FROM nginx:latest

COPY nginx.conf /etc/nginx/nginx.conf
COPY my_nginx.conf /etc/nginx/sites_available/

RUN mkdir -p /etc/nginx/sites_enabled/\
        && ln -s /etc/nginx/sites_available/my_nginx.conf /etc/nginx/sites_enabled

CMD ["nginx", "-g", "daemon off;"]
