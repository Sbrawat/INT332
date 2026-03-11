# Convert the given file into docker compose :
```docker
 FROM wordpress:latest
```
## Set environment variables for database connection
```docker

ENV WORDPRESS_DB_HOST=db
ENV WORDPRESS_DB_USER=wpuser
ENV WORDPRESS_DB_PASSWORD=wppassword
ENV WORDPRESS_DB_NAME=wpdatabase
```
## Expose port
```docker
EXPOSE 80
```
## With docker run command :m
```bash
docker run -d \
--name wordpress_app \
-p 8082:80 \
-e WORDPRESS_DB_HOST=db \
-e WORDPRESS_DB_USER=wpuser \
-e WORDPRESS_DB_PASSWORD=wppassword \
-e WORDPRESS_DB_NAME=wpdatabase \
-v wordpress_data:/var/www/html \
mywordpress
```