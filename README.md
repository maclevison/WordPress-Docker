# WordPress-Docker

### Project config
---

Install Docker https://www.docker.com/get-started

#### Create project directory

```
$ mkdir your-project-name
$ cd your-project-name
```
 
Create _docker-compose.yml_ file in the root directory

```
$ touch docker-compose.yml
```
Copy & Paste following code into _docker-compose.yml_ file.
```
version: '3.3'

services:
  db:
    image: mysql:5.7
    ports:
      - "3308:3306"
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - "9000:80"
    volumes:
      - ./app:/var/www/html # Full wordpress project
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
volumes:
  db_data:
```

#### Running the project

```
$ docker-compose up -d
```  

#### Shutdown the project

```
$ docker-compose down
```  
