Side Self Study
Make yourself familiar with basic SQL syntax and most commonly used commands
Be comfortable using not only VIM, but also Nano editor as well, get to know basic Nano commands

INSTALLING NGINX WEB SERVER
Nginx a high performance web server
    sudo apt update
    sudo apt install nginx



install mysql-server 

run a script from mysql to remove => This script will remove some insecure default settings and lock down access to your database system. Start the interactive script by running:

"sudo mysql_secure_installation"

test myqsl with " sudo mysql "  exit to exit the shell

Installing php


While Apache embeds the PHP interpreter in each request, Nginx requires an external program to handle PHP processing and act as a bridge between the PHP interpreter itself and the web server. This allows for a better overall performance in most PHP-based websites, but it requires additional configuration. You’ll need to install php-fpm, which stands for “PHP fastCGI process manager”, and tell Nginx to pass PHP requests to this software for processing. Additionally, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies.

sudo apt install php-fpm php-mysql

php -v to check the verions

CONFIGURING NGINX TO USE PHP PROCESSOR

nginx is confiured to serve from "var/www/html."

sudo mkdir /var/www/projectLEMP
sudo chown -R $USER:$USER /var/www/projectLEMP

sudo nano /etc/nginx/sites-available/projectLEMP
#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}


listen — Defines what port Nginx will listen on. In this case, it will listen on port 80, the default port for HTTP.
root — Defines the document root where the files served by this website are stored.
index — Defines in which order Nginx will prioritize index files for this website. It is a common practice to list index.html files with a higher precedence than index.php files to allow for quickly setting up a maintenance landing page in PHP applications. You can adjust these settings to better suit your application needs.
server_name — Defines which domain names and/or IP addresses this server block should respond for. Point this directive to your server’s domain name or public IP address.
location / — The first location block includes a try_files directive, which checks for the existence of files or directories matching a URI request. If Nginx cannot find the appropriate resource, it will return a 404 error.
location ~ \.php$ — This location block handles the actual PHP processing by pointing Nginx to the fastcgi-php.conf configuration file and the php7.4-fpm.sock file, which declares what socket is associated with php-fpm.
location ~ /\.ht — The last location block deals with .htaccess files, which Nginx does not process. By adding the deny all directive, if any .htaccess files happen to find their way into the document root ,they will not be served to visitors.

Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:

sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/

TO TEST NGINX CONFIGURATION FOR ERRORS

sudo nginx -t

We also need to disable default Nginx host that is currently configured to listen on port 80, for this run:

"sudo unlink /etc/nginx/sites-enabled/default
"

sudo systemctl reload nginx

connecting to mysql

sudo mysql

craete a user with a password in mysql
mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';

grant user to a database
mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';

to login with a users account
mysql -u example_user -p

TO LIST databases
SHOW DATABASES;


CREATE TABLE example_database.todo_list (
     item_id INT AUTO_INCREMENT,
     content VARCHAR(255),
     PRIMARY KEY(item_id)
);

INSERT INTO example_database.todo_list (content) VALUES ("My first important item");

SELECT * FROM example_database.todo_list;


NGINX pronounced as (engine-x)

http://18.223.196.69/
http://18.223.196.69/todo_list.php
http://18.223.196.69/info.php