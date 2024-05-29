# Deploying WordPress on AWS

I recently deployed WordPress on AWS using a straightforward approach. Here are the main steps:

## Step 1: Create an Instance

- Launch a new EC2 instance on AWS.
- Choose an appropriate AMI (e.g., Ubuntu Server).
- Configure instance details, add storage, and set security groups (allow HTTP, HTTPS, and SSH).

## Step 2: Connect to the Apache Server

- Connect to your instance using PuTTY (for Windows) or SSH (for Linux/Mac).
- Update package lists:

```bash
sudo apt update
```

- Install Apache:

```bash
sudo apt install apache2
```

- Enable Apache to start on boot and start the service:

```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

## Step 3: Connect to the RDS

- Create an RDS instance (MySQL) on AWS.
- Note down the endpoint, database name, username, and password.
- Install MySQL client on your EC2 instance:

```bash
sudo apt install mysql-client
```

- Test connection to RDS:

```bash
mysql -h your-rds-endpoint -u your-username -p
```

## Step 4: Deploy WordPress

- Navigate to Apache's web root directory:

```bash
cd /var/www/html
```

- Download WordPress:

```bash
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xvzf latest.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
```

- Set correct permissions:

```bash
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```

- Create a wp-config.php file:

```bash
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
```

- Edit wp-config.php with your database details:

```php
define('DB_NAME', 'your-database-name');
define('DB_USER', 'your-username');
define('DB_PASSWORD', 'your-password');
define('DB_HOST', 'your-rds-endpoint');
```

- Complete the WordPress installation by accessing your domain or public IP in a web browser and following the setup wizard.

## Tools Used

- Apache Web Server: To deploy WordPress.
- PuTTY: To connect to and manage the Ubuntu instance.

##All Commands
# Step-by-Step Guide to Deploy WordPress on Ubuntu

Follow these steps to deploy WordPress on Ubuntu:

1. **Install Apache server on Ubuntu**

    ```bash
    sudo apt install apache2
    ```

2. **Install php runtime and php mysql connector**

    ```bash
    sudo apt install php libapache2-mod-php php-mysql
    ```

3. **Install MySQL server**

    ```bash
    sudo apt install mysql-server
    ```

4. **Login to MySQL server**

    ```bash
    sudo mysql -u root
    ```

5. **Change authentication plugin to mysql_native_password (change the password to something strong)**

    ```sql
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'Testpassword@123';
    ```

6. **Create a new database user for WordPress (change the password to something strong)**

    ```sql
    CREATE USER 'wp_user'@localhost IDENTIFIED BY 'Testpassword@123';
    ```

7. **Create a database for WordPress**

    ```sql
    CREATE DATABASE wp;
    ```

8. **Grant all privileges on the database 'wp' to the newly created user**

    ```sql
    GRANT ALL PRIVILEGES ON wp.* TO 'wp_user'@localhost;
    ```

9. **Download WordPress**

    ```bash
    cd /tmp
    wget https://wordpress.org/latest.tar.gz
    ```

10. **Unzip**

    ```bash
    tar -xvf latest.tar.gz
    ```

11. **Move WordPress folder to Apache document root**

    ```bash
    sudo mv wordpress/ /var/www/html
    ```

12. **Command to restart/reload Apache server**

    ```bash
    sudo systemctl restart apache2
    ```

    OR

    ```bash
    sudo systemctl reload apache2
    ```

13. **Install certbot**

    ```bash
    sudo apt-get update
    sudo apt install certbot python3-certbot-apache
    ```

14. **Request and install SSL on your site with certbot**

    ```bash
    sudo certbot --apache
    ```

Follow these steps to set up WordPress on Ubuntu successfully. 


By following these steps, you can deploy WordPress on AWS with ease. Happy blogging! #AWS #WordPress #CloudDeployment #Apache #PuTTY #RDS #Ubuntu
