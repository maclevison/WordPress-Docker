# WordPress-Docker

#### Project config

Install Docker https://www.docker.com/get-started

**1 - Create an empty project directory**

```
mkdir your-project-name
cd your-project-name
```

**2 - Create a _docker-compose.yml_ file in the root directory**

```
touch docker-compose.yml
```

**3 - Copy & Paste following code into _docker-compose.yml_ file.**

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

**4 - Build the project**

Run following command from your project directory.

```
docker-compose up -d
```  

**5 - Bring up WordPress in a web browser**

If you are using Docker Desktop for Mac or Docker Desktop for Windows, you can use http://localhost as the IP address, and open http://localhost:9000 in a web browser.

**6 - Shutdown**

```
docker-compose down
```  

**Cleanup**

The command ``docker-compose down --volumes`` removes the containers, default network, and the WordPress database.

---
Learn more: https://docs.docker.com/compose/wordpress/