# YML

```yaml
version: '3.8'

services:
# database
  db:
    image: mysql:5.7
    container_name: db
    volumes:
      - db_data_volume:/var/lib/mysql
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    networks:
      - dockerwp
# overlay for database
  phpmyadmin:
    depends_on:
      - db
    image: phpmyadmin
    container_name: phpmyadmin
    restart: unless-stopped
    #ports:
     # - "8080:80"
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: password
    networks:
      - dockerwp
# website editor 
  wordpress:
    depends_on:
      - db
      - app
    image: wordpress:latest
    container_name: wp
    volumes:
      - wordpress_data_volume:/var/www/html
    #  - ./src:/var/www/html
   # ports:
     # - '8000:80'
    restart: unless-stopped
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
    networks:
      - dockerwp
# nginx proxy manager
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'    # Public HTTP Port
      - '443:443'  # Public HTTPS Port
      - '81:81'    # Admin Web Port
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
    networks:
      - dockerwp

# my network
networks:
  dockerwp:
    driver: bridge
    name: proxy

volumes:
  db_data_volume: {}
  wordpress_data_volume: {}
```
