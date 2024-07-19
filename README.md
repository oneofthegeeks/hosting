# Setting Up Hosting Server on VM

Follow these steps to set up a hosting server on a Virtual Machine (VM) using Docker and Docker Compose.

## Prerequisites

Ensure your VM is running an updated version of Ubuntu.

## Steps

1. **Update the package list:**
    ```bash
    sudo apt update
    ```

2. **Install Docker and Docker Compose:**
    ```bash
    sudo apt install docker.io docker-compose -y
    ```

3. **Create a directory for the WordPress site:**
    ```bash
    mkdir -p ~/wordpress/oneofthegeeks
    ```

4. **Create and edit the Docker Compose file:**
    ```bash
    sudo nano ~/wordpress/oneofthegeeks/docker-compose.yml
    ```

5. **Copy the following code into the `docker-compose.yml` file:**

    ```yaml
    version: '3.7'

    services:
      wordpress:
        image: wordpress:latest
        container_name: wordpress_oneofthegeeks
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
        container_name: mysql_oneofthegeeks
        restart: always
        environment:
          MYSQL_DATABASE: wordpress
          MYSQL_USER: wordpress
          MYSQL_PASSWORD: wordpress
          MYSQL_ROOT_PASSWORD: root_password
        volumes:
          - ./db_data:/var/lib/mysql
    ```

    **Note:** Change the port by 1 (e.g., "8082:80") if setting up multiple sites.

6. **Navigate to the WordPress directory:**
    ```bash
    cd ~/wordpress/oneofthegeeks
    ```

7. **Start the Docker containers:**
    ```bash
    sudo docker-compose up -d
    ```

## Conclusion

You have now set up a WordPress site on your VM using Docker and Docker Compose. Access your site by navigating to your VM's IP address and the specified port (e.g., `http://your_vm_ip:8081`).

For additional sites, repeat steps 3-7, adjusting the port number in the `docker-compose.yml` file accordingly.
