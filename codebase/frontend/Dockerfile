# Dockerfile to host the files as a web server 
FROM nginx:alpine
# Should be using nginx with the html and js files moved over to the default nginx location /usr/share/nginx/html
COPY index.html /usr/share/nginx/html/index.html

COPY index.js /usr/share/nginx/html/index.js

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
