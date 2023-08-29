# Select base image for container
FROM alpine:3.16

# Update Alpine Package Keeper and install nginx and openssl
RUN apk update && apk add nginx openssl

# Create required directories inside container (location for files to be served, ssl key)
RUN mkdir -p /var/www/html /run/nginx /etc/nginx/ssl
# NOTE: Confirm what the /run/nginx directory is used for

# Copy config file for nginx
COPY /conf/nginx.conf /etc/nginx/http.d/default.conf

# Create SSL keys
RUN openssl req -newkey rsa:2048 -x509 -sha256 -days 365 -nodes \
    -out /etc/nginx/ssl/sslcert.crt \
    -keyout /etc/nginx/ssl/sslcert.key \
    -subj "/C=CA/ST=Quebec/L=Quebec/O=42School/OU=42Quebec/CN=jgoad.42.fr"

# Start nginx
CMD [ "nginx", "-g", "daemon off;" ]