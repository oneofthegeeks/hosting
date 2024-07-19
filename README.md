# hosting
Setting up hosting server VM instructions and steps



sudo apt update
sudo apt install docker.io docker-compose -y
mkdir -p ~/wordpress/site1
sudo nano ~/wordpress/site1/docker-compose.yml

#Copy in the following code to the yml file and change the port by 1 if doing multiple sites

version: '3.7'

services:
  wordpress:
    image: wordpress:latest
    container_name: wordpress_site1
    restart: always
    ports:
      - "8081:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - ./wordpress:/var/www/html

  db:
    image: mysql:5.7
    container_name: mysql_site1
    restart: always
    environment:
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
      MYSQL_ROOT_PASSWORD: root_password
    volumes:
      - ./db_data:/var/lib/mysql


## End of Copy 

cd ~/wordpress/site1
sudo docker-compose up -d


