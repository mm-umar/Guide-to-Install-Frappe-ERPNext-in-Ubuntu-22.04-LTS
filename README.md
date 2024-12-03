
# Guide-to-Install-Frappe-ERPNext-in-Ubuntu-22.04-LTS
A complete Guide to Install Frappe Bench in Ubuntu 22.04 LTS and install Frappe/ERPNext Application

### STEP 1 Install git
    sudo apt-get install git

### STEP 2 install python-dev

    sudo apt-get install python3-dev

### STEP 3 Install setuptools and pip (Python's Package Manager).

    sudo apt-get install python3-setuptools python3-pip

### STEP 4 Install virtualenv
    
    sudo apt-get install virtualenv
    
  CHECK PYTHON VERSION 
  
    python3 -V
  
  IF VERSION IS 3.8.X RUN
  
    sudo apt install python3.8-venv

  IF VERSION IS 3.10.X RUN
  
     sudo apt install python3.10-venv

### STEP 5 Install MariaDB

Install software-properties-common package using apt-get

    sudo apt-get install software-properties-common

Install mariadb-server package using apt

    sudo apt install mariadb-server

Run the mysql_secure_installation command with root privileges

    sudo mysql_secure_installation
    
    
### STEP 6  MySQL database development files

    sudo apt-get install libmysqlclient-dev

### STEP 7 Edit the mariadb configuration ( unicode character encoding )

    sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf

add this to the 50-server.cnf file

This is read by the standalone daemon and embedded servers

    [server]
    user = mysql
    pid-file = /run/mysqld/mysqld.pid
    socket = /run/mysqld/mysqld.sock
    basedir = /usr
    datadir = /var/lib/mysql
    tmpdir = /tmp
    lc-messages-dir = /usr/share/mysql
    bind-address = 127.0.0.1
    query_cache_size = 16M
    log_error = /var/log/mysql/error.log

This is only for the mysqld standalone daemon
    
    [mysqld]
    innodb-file-format=barracuda
    innodb-file-per-table=1
    innodb-large-prefix=1
    character-set-client-handshake = FALSE
    character-set-server = utf8mb4
    collation-server = utf8mb4_unicode_ci      

Comment out these two lines (add # at the beginning of the line)

    character-set-server  = utf8mb4
    collation-server      = utf8mb4_general_ci

append to the end of the file.

    [mysql]
    default-character-set = utf8mb4

Now press (Ctrl-X) to exit

    sudo service mysql restart

### STEP 8 install Redis
    
    sudo apt-get install redis-server

### STEP 9 install Node.js 16.X package

Install curl package using apt

    sudo apt install curl 

Download and run the installation script for nvm from the GitHub repository

    curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash

Load the updated environment variables from the .profile file

    source ~/.profile
    
Install Node.js version 18.16.1 using nvm    
    
    nvm install 18.16.1  

### STEP 10  install Yarn

Install npm package using apt-get

    sudo apt-get install npm

Install yarn globally using npm

    sudo npm install -g yarn

### STEP 11 install wkhtmltopdf

    sudo apt-get install xvfb libfontconfig wkhtmltopdf
    

### STEP 12: Install Frappe Bench

If the first command doesn't work, try the second one:
	
	sudo -H pip3 install frappe-bench

If that doesn't work, use the following command:
	
	sudo -H pip3 install frappe-bench --break-system-packages

Check version
    
    bench --version
    
### STEP 13 initilise the frappe bench & install frappe latest version 

Initilise the frappe bench

    bench init frappe-bench 

Move to the frappe-bench directory

    cd frappe-bench/

Start bench

    bench start
    
### STEP 14 create a site in frappe bench 

Create new site

    bench new-site my-site

Use created site
    
    bench use my-site

### STEP 15 install ERPNext latest version in bench & site


    bench get-app erpnext --branch version-14
OR

    bench get-app https://github.com/frappe/erpnext --branch version-14

Install ERPNext app

    bench --site my-site install-app erpnext

Start bench
    
    bench start
