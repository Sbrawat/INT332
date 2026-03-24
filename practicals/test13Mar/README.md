# Practice Questions on Docker Compose

## Q1 Modify the following given Docker Compose file to:

1. Map port 8081 on host to port 80 in container
2. Mount a local folder ./website to usr/lcoal/apache2/htdocs
3. Set container name as apache_server

### Docker Compose File

```yaml
version:"3"
services:
    web:
    image: httpd
```

## Q2 creat a docker-compose.yml file to deply the following application

### Requirements

1. Service 1 Nginx web server
   ```
   image: nginx
   Port Mapping: 8085:80
   ```
2. Service 2: Redis Database
   ```
   image: redis
   ```
3. Both services must:
4. Run on a custom network appnetwork\
5. The nginx container name should be nginx_server
