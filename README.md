#  ![836974 (2)](https://user-images.githubusercontent.com/103517339/221184251-18f51e1c-c91d-4d6c-b58a-ca7848d10252.jpg) INSTALLING FRAPPE DRIVE

A complete Guide to Install Frappe Drive in Ubuntu 22.04 LTS.

All the commands mentioned here has to be RUN IN TERMINAL.

### First of all , run these commands before installing the drive
    sudo apt update
###     
    sudo add-apt-repository universe
###
    sudo add-apt-repository multiverse
###
    sudo apt update
After running these commands, move on to the Steps.

### STEP 1 Install git
    sudo apt-get install git

### STEP 2
  Press y when asked Do you want to continue
###
    sudo apt-get install python3-dev

### STEP 3

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

    sudo apt-get install software-properties-common
### 
    sudo apt install mariadb-server
### 
    sudo mysql_secure_installation

 
Press Enter here and press y on both( switch to unix_socket authentication & change the root password)

![Untitled design (4)](https://user-images.githubusercontent.com/103517339/221205790-8c0d83ee-0ed3-4cbf-b017-efd28d3728f4.png)

Set a password after running this command.

Press y every time it asks

    
    
### STEP 6

    sudo apt-get install libmysqlclient-dev

### STEP 7 Edit the mariadb configuration

    sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf


  Add this in a next line under the word [server] like this
  
  
  ![image](https://user-images.githubusercontent.com/103517339/221207997-f92eb101-e77b-40ab-ac94-128dcff3e8ca.png)

     
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
    
  Add this in a next under the word [mysqld] like this
  
  
  ![image](https://user-images.githubusercontent.com/103517339/221208100-548b0728-3018-43b1-bbc0-cf7da2f406bd.png)

    
    
    innodb-file-format=barracuda
    innodb-file-per-table=1
    innodb-large-prefix=1
    character-set-client-handshake = FALSE
    character-set-server = utf8mb4
    collation-server = utf8mb4_unicode_ci   
   
   Comment this lines by putting a # at the front of the line 
   
   
   ![Untitled design (5)](https://user-images.githubusercontent.com/103517339/221209134-1fedcb22-d16b-403d-b7f2-11164baeaef9.png)

     
   Add this at the last.
###
    [mysql]
    default-character-set = utf8mb4

Now press (Ctrl-X) to exit and restart the mysql by running this command.

    sudo service mysql restart

### STEP 8 Install Redis
    
    sudo apt-get install redis-server

### STEP 9 Install Node.js and npm using NVM
  Install NVM tool
###
    sudo apt install curl 
###
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
###    
If there is a error like this: curl: (35) OpenSSL SSL_connect: Connection reset by peer in connection to raw.githubusercontent.com:443
Then try running this command first and then try the previous command.
###
    openssl s_client -connect github.com:443 -servername github.com
###
    source ~/.bashrc
### 
    nvm --version
    
###
    nvm install v16.19.0
###
   After installing node, check the installed version
###
    node --version

### STEP 10  install Yarn

    sudo apt-get install npm
###
    sudo npm install -g yarn

### STEP 11 install wkhtmltopdf

    sudo apt-get install xvfb libfontconfig wkhtmltopdf
    

### STEP 12 install frappe-bench

    sudo -H pip3 install frappe-bench

Check the installed version of bench
 ### 
    bench --version
    
### STEP 13 

    bench init frappe-bench --frappe-branch version-14
###
    cd frappe-bench/

  start the bench
###
    bench start
     
### STEP 14 

copy the url written after ruuning on ( for example - "http://192.168.226.130:8000/") and run it on browser.


![Untitled design (3)](https://user-images.githubusercontent.com/103517339/221194437-3376dd92-f45a-4b78-9221-a0e1a7f3e43f.png)


NOT FOUND will be displayed on this site.


Open a new terminal tab from top left button  ![Screenshot 2023-02-24 191138 (2)](https://user-images.githubusercontent.com/103517339/221193423-4cc90626-65db-49b6-a35c-5f4d27d55178.jpg)

### STEP 15
Run this in new terminal which we just opened in the last step.

    bench get-app https://github.com/frappe/drive
    
###
    bench new-site drive.site
    
  Here you may need to enter Mysql password which you created earlier.
  Also you will create Administrator password here.
###
    bench use drive.site
###
    bench migrate
###
    bench --site drive.site add-to-hosts
###
    bench --site drive.site install-app drive
###
    cd apps/drive && yarn dev

    
 Now move to the previous tab in teminal and restart the bench 
 ###
     bench  start
     
 Now open the browser and reload the site( refer step 14)
 
 ![image](https://user-images.githubusercontent.com/103517339/221199355-bcece20d-65dc-4914-892d-e9f7d210b3c1.png)
 
 It will appear like this, Enter Administrator as username and the password should the same as created in step 15.
 
 Finally, open the URL http://drive.site:8000/drive in your browser to see the app running.
 ###
   Frappe Drive is running now.


    

    
