FROM nginx:1.13.12

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx

EXPOSE 80

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]