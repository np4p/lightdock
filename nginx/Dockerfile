ARG NGINX_VERSION
FROM nginx:${NGINX_VERSION}

ARG TZ=PRC
ENV TZ ${TZ}

COPY nginx.conf /etc/nginx/
COPY conf.d/ /etc/nginx/conf.d/

# Create 'messages' file used from 'logrotate'
RUN touch /var/log/messages

# Copy 'logrotate' config file
COPY logrotate/nginx /etc/logrotate.d/

CMD ["nginx"]

EXPOSE 80 443
