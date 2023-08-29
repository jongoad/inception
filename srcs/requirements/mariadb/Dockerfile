# Select base image for container
FROM alpine:3.16

# Update an upgrade Alpine Package Keeper and install mariadb as well as mariadb-client
RUN apk update && apk upgrade && apk add mariadb mariadb-client

# Clear any previous mariadb conf files
RUN rm -rf /etc/my.cnf

# Copy newest version of my.cnf into container
COPY config/my.cnf /etc/my.cnf

# Create required directories inside container
RUN mkdir -p /run/mysqld

# Change file ownership for directories (-R is recursive mode, works on all files and directories from target down, mysql:mysql is owner:group) 
RUN chown -R mysql:mysql /run/mysqld; \
    chown -R mysql:mysql /var/lib/mysql

# Install mariadb (mysql_install_db is a symlink to the binary mariadb-install-db)
RUN	mysql_install_db --basedir=/usr --user=$MYSQL_USER --datadir=/var/lib/mysql

# Runs setup script
COPY docker-entrypoint.sh /tmp/docker-entrypoint.sh
ENTRYPOINT [ "sh", "/tmp/docker-entrypoint.sh" ]

# Loads mysqld as PID 1 (mysqld in this binary for the mySQL server)
CMD [ "mysqld" ]
