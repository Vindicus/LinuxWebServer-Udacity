# Linux Web Server Configuration
## Description:
----------------
Configure and transform a Linux based server to a web server and host the YumYumRecipes application.

## IP Address, SSH Port, Remote User
-------------------------------------
IP address: <http://35.160.24.80/>  
SSH Port: 2200  
Remote User: `grader`
Remote Password: `grader`

## Postgresql Access
---------------------
### User1 Access:
User: `postgres`
password: `postgres`

### User2 Access:
User: `cataog`
password: `catalog`

## Remote Machine Access
-------------------------
Access: ssh -i ~/.ssh/udacity_key.rsa root@35.160.24.80 -p 2200

## Configuration changes
-------------------------

### Adding user
1. Create user 'grader'
        adduser grader
2. Create sudoers.d file and grant 'grader' 'sudo' access
        nano /etc/sudoers.d/grader
    Resource: <http://askubuntu.com/questions/334318/sudoers-file-enable-nopasswd-for-user-all-commands>
3. Generate SSH key for grader on local machine
        ssh-keygen in ~/.ssh/grader
4. Copy the SSH key in authorized_keys file
        store file in /home/grader/.ssh/authorized_keys
        
### Change default SSH port to 2200
1. Configure /etc/ssh/sshd_config
        set port from 22 to 2200
        
### Set RemoteRootLogin to No
1. Configure /etc/ssh/sshd_config
        set RemoteRootLogin from without-password to No
    Resource: <https://mediatemple.net/community/products/dv/204643810/how-do-i-disable-ssh-login-for-the-root-user>
    
### Update and upgrade existing packages
1. update packages file to latest package versions
        sudo apt-get update
2. Upgrade existing packages
        sudo apt-get upgrade
        
### Configure UFW firewall
1. Allow SSH port 2200, HTTP port 80, NTP port 123
        sudo ufw allow 2200/tcp
        sudo ufw allow www
        sudo ufw allow 123/udp
2. Activate UFW firewall
        sudo ufw enable
    Reference: Udacity
    
### Configure Time to UTC
1. Set timezone to UTC
        sudo dpkg-reconfigure tzdata
    Reference: <http://unix.stackexchange.com/questions/110522/timezone-setting-in-linux>
    
### Python-Flask application deployment
1. Git clone <https://github.com/Vindicus/YumYumRecipes.git>
2. rename 'main.py' file to '__init__.py'
        mv main.py __init__.py
3. Configure virtual host
        sudo nano /etc/apache2/sites-available/YumYumRecipes.conf
    Reference: <https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps>
4. Create WSGI file
        sudo nano /var/www/YumYumRecipes/YumYumRecipes.wsgi
    Reference: <https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps>

## List of software installed
------------------------------
1. 'sudo apt-get install' apache2
2. 'sudo apt-get install' libapache2-mod-wsgi
3. 'sudo apt-get install' git
4. 'sudo apt-get install' python-pip
5. 'pip install' virtualenv
6. 'pip install' Flask
7. 'pip install'  oauth2client
8. 'pip install'  requests
9. 'pip install'  httplib2
10. 'sudo apt-get install' postgresql
11. 'pip install' sqlalchemy
12. 'pip install' psycopg2
13. 'pip install' python-psycopg2
