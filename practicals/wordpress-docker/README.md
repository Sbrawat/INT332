# Run Wordpress and MySQL services using Docker Compose

## Architecutre of the App​
1. user Browser -> localhost
2. WordPress Container -> MySQL Connection
3. MySQL Container -> Database Storage (Volume)

## Create Project Directory​
```console
mkdir wordpress docker
cd wordpress-docker
```

## Create Docker Compose File (YAML)
```YAML
services:
  wordpress:
    image: wordpress:latest
    container_name: wordpress_app
    restart: always
    ports:
      -"8082:80"
    environment:
    WORDPRESS_DB_HOST: db
    WORDPRESS_DB_USER: wpuser
    ​WORDPRESS_DB_PASSWORD: wppassword
    WORDPRESS_DB_NAME: wpdatabase
    volumes:
      -wordpress_data:/var/www/html
    depends_on:
      -db

  db:
    image: mysql:5. 7
    container_name: wordpress_db
    restart: always
    environment:
    MYSQL_DATABASE: wpdatabase
    MYSQL_USER: wpuser
    MYSQL_PASSWORD: wppassword
    MYSQL_ROOT_PASSWORD: rootpassword

    volumes:
      -db_data:/var/lib/mysql

volumes: 
  wordpress_data:
  db_data:
```

## docker compose up -d

## Access Wordpress