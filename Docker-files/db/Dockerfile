FROM mysql:8.0.33

LABEL "Project"="Vprofile"
LABEL "Author"="Olayinka"

# Security: Set initial database credentials via environment variables
ENV MYSQL_ROOT_PASSWORD="vprodbpass"
ENV MYSQL_DATABASE="accounts"

# Automatically initialize the database with your backup script
ADD db_backup.sql /docker-entrypoint-initdb.d/db_backup.sql

# Security: Ensure MySQL is running as the default mysql user (UID 999)
# This is handled by the base image, but it's good practice to verify.
USER mysql

EXPOSE 3306
