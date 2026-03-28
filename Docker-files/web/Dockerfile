FROM nginx:1.27-alpine

LABEL "Project"="Vprofile"
LABEL "Author"="Olayinka"

# Security: Remove default Nginx config and set custom one
RUN rm -rf /etc/nginx/conf.d/default.conf
COPY nginvproapp.conf /etc/nginx/conf.d/vproapp.conf

# Security: Set ownership for nginx user to run on non-privileged port
RUN chown -R nginx:nginx /var/cache/nginx /var/log/nginx /etc/nginx/conf.d /var/run && \
    touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid

# Security: Switch to the nginx user
USER nginx

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
