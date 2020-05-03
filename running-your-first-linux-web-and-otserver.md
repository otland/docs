# Running your first ubuntu linux OT

## Getting started

Rent a Ubuntu Server 18.04 or higher from a trusted hosting company such or install for the sake of learning experience Ubuntu Server 18.04 or higher in VirtualBox.

Once you're set we will start by accessing our server. If you're on windows you should get putty\([https://www.putty.org/](https://www.putty.org/)\), if you're on macOS or Linux you can use the terminal which is standard available. With putty just follow the screen \( insert your domain/ip-address and click ok \) for macOS and linux users type:

```bash
ssh username@domain/ipaddress
```

`username example => root domain/ipaddress example => yourdomain.com or 127.0.0.1`

Now you will be prompted for your password \(if in putty you will be prompted for the password as soon you click on Open\) Insert your password and presh enter \(you will not see what you type, so make sure you type your password in the right order\). Now we are in our server :\)

### Update and Upgrade the system

The first thing we will do is updating our Ubuntu Server with the following command

```bash
sudo apt update && sudo apt upgrade -y
```

We are using 'sudo' since I do not know if you're running as root user or as regular user. When you're logged in as regular user. No problem! Just enter your password when the terminal asks for your password. With the command above you will update the connected repository's the server is connected to and when the server is done updating the repository's it will directly upgrade all the packages which were updated.

## Installing the webserver

Now we will get to the more difficult part of the entire server setup, installing nginx, php-fpm, mariadb-server with phpmyadmin.

```bash
sudo apt install nginx php-fpm mariadb-server -y
```

The installation process is now triggered.When this is finished we will install phpmyadmin to handle our database server \(which is mariadb\)

```bash
sudo apt install phpmyadmin -y
```

Now we are set to get some configurations going!

### Configuring the webserver

First we want to know which version of php-fpm is installed we will check this by writing the following command in the terminal

```bash
sudo php -v
```

The output will be looking something similar as this \(I am using ubuntu 19.10 here which uses php version 7.3 as default. If you're running on a server you most likely run on 18.04 lts or with the newest version 20.04 lts\):

![phpversion](https://worldofcoding.net/github-img/otland-gitbook/phpversion.png)

Second we want to do is enabling php in our nginx server and setting the configuration just as we want. So we will be going to edit our nginx config. Now we need to install a command line text editor called "vim". After that we installed it we will directly open the configuration file.

```bash
sudo apt install vim -y && sudo vim /etc/nginx/sites-available/default
```

Now sit straight up and read carefully on what we're going to do. I am going to give you a few options in the configuration. Underneath here you will find the default configuration file of nginx. \( I only took the part of the config file we are in need to use and left out all the comments which we do use in this tutorial \)

### Changing the web-root

We can change the 'root' directory of the website folder, if you're only using your server as root leave it in '/var/www/html'. When using it as for example 'john' you can change the directory to your default directory when you come when you login which is: '/home/john' in the default directory of john you can do 'mkdir www' to create a directory for the website and set: '/home/john/www' on line '5' instead of '/var/www/html'.

### Configuring php

I already enabled php here by writing 'index.php' on line number '24'. I've uncommented the php location settings we need to use. To make it easy and understanding I made own comments for you guys to know which lines to comment and uncomment, depending on which Ubuntu Server version you are running \( and assuming you're using Ubuntu Server 18.04 lts \).

```bash
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /var/www/html;

        # Add index.php to the list if you are using PHP
        index index.php index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }

        # pass PHP scripts to FastCGI server
        #
        location ~ \.php$ {
               include snippets/fastcgi-php.conf;
        #
        #       # With php-fpm (or other unix sockets):
        ################## UBUNTU 18.04 LTS ##################
               fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        ################## UBUNTU 20.04 LTS ##################
        #       fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;

        }

}
```

Now we have to save the file and quit the file, we do this the following way: `CTRL+C` After that you will just write `:wq` press enter and we have saved and quit the file :\)

We are set with the entire webserver now and so its time to check if we actually did everything as we supposed to do, but first we have to restart our web features. We do this with the following commands: `Change the number of the php-fpm version to one you're using!!!`

```bash
sudo systemctl restart nginx
sudo systemctl restart php7.2-fpm
```

Lets open our browser and goto your ip-address and see how wonderful you are! Your very own setup and configured server!

## Setup the database user + phpmyadmin

We need to create ourselves a mysql admin account. We will be doing this the following way. Please follow the steps carefully :\)

```bash
sudo mariadb
```

![phpversion](https://worldofcoding.net/github-img/otland-gitbook/phpversion.png)

#### You are inside the database right now!

We will be creating the user 'otadmin' with the password of 'otadminpassword', change these values to what you want it to be!

```bash
create user 'otadmin'@'localhost' identified by 'otadminpassword';
grant all privileges on *.* to 'otadmin'@'localhost';
flush privileges;
exit;
```

Insert these lines one by one. Now we have setup our database superuser :\)

### Configure phpmyadmin

Setup phpmyadmin to access your database via the browser.

Insert the following configuration in a new file inside the nginx folder. The following command will create the file and when you are in insert the configuration posted below. \( same as for the webserver nginx configuration I have made comments for the ubuntu versions inside the php location \) `sudo vim /etc/nginx/sites-available/phpmyadmin`

```bash
server {
    listen      2344;
    server_name  _;
    root /usr/share/phpmyadmin;

    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;
    add_header X-XSS-Protection "1; mode=block";

    client_max_body_size 256M;
    error_page 404 @notfound;

    location / {
        index index.html index.php;
        try_files $uri $uri/ /index.php?$args;
    }

    location ~* \.(gif|jpg|jpeg|png|bmp|js|css)$ {
        expires max;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;

    ################## UBUNTU 18.04 LTS ##################
           fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
    ################## UBUNTU 20.04 LTS ##################
    #       fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;

    }

    location @notfound {
        return 404 "You're not browsing correctly.";
        add_header Content-Type text/plain always;
    }

}
```

Now we have to save the file and quit the file, we do this the following way: `CTRL+C` After that you will just write `:wq` press enter and we have saved and quit the file :\)

Now we have to enable the phpmyadmin configuration for nginx we do that by running the next command: `sudo ln -s /etc/nginx/sites-available/phpmyadmin /etc/nginx/sites-enabled/phpmyadmin`

Finally restart the nginx server with `sudo systemctl restart nginx` and we will be able to access phpmyadmin by [http://youripordomain:2344](http://youripordomain:2344) login with the database username and password we've created.

## Setup your Server for TFS

First of all we need to install a few packages to our system which makes us able to build the TFS sources.

Directly copy'd from the TFS github wiki\([https://github.com/otland/forgottenserver/wiki/Compiling-on-Ubuntu](https://github.com/otland/forgottenserver/wiki/Compiling-on-Ubuntu)\):

### Install the required software

The following command will install Git, CMake, a compiler and the libraries used by The Forgotten Server.

Git will be used to download the source code, and CMake will be used to generate the build files.

```bash
sudo apt-get install git cmake build-essential liblua5.2-dev libgmp3-dev libmysqlclient-dev libboost-system-dev libboost-iostreams-dev libboost-filesystem-dev libpugixml-dev libcrypto++-dev
```

### Download the source code

```bash
git clone --recursive https://github.com/otland/forgottenserver.git
```

### Generate the build files

```bash
cd forgottenserver
mkdir build && cd build
cmake ..
```

### Build

```bash
make
```

