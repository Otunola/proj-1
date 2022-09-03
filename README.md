# proj-1 LAMP STACK IMPLEMENTATION

1. The first step is to Install Apache using Ubuntu’s package manager ‘apt’ on our UBuntu server we created with the command : sudo apt update

2. Then run the apache with this command : sudo apt install apache2
3. we check the status of our installation with the command. : sudo systemctl status apache2
below is our output

<img width="573" alt="Screen Shot 2022-09-03 at 10 41 52 AM" src="https://user-images.githubusercontent.com/112595648/188265291-962b6d14-c53f-4767-acf7-95babfcafcab.png">

4. I made sure TCP port 80 is opened to the internet by adjusting the inbound rules on the the instance security group as shown below:

<img width="1133" alt="Screen Shot 2022-09-03 at 10 54 29 AM" src="https://user-images.githubusercontent.com/112595648/188265524-45182c5f-165b-4a71-bd3a-4a6a84f24c17.png">

5. Then i can confirm my port 80 is opened by running the command : curl http://127.0.0.1:80 
which then gave the output below
<img width="568" alt="Screen Shot 2022-09-03 at 11 00 48 AM" src="https://user-images.githubusercontent.com/112595648/188265718-998c2c5d-8277-4a3a-9235-4194adf874c4.png">

6. I tested the apache web server by entering the public address of my server on the url 3.251.91.230 and i got the output below

<img width="1245" alt="Screen Shot 2022-09-03 at 11 03 51 AM" src="https://user-images.githubusercontent.com/112595648/188265792-c56c1ff2-e660-4281-9ddd-3cc85df1e3b9.png">

7. I installed Mysql server with the commmand: sudo apt install mysql-server

8. i coonected to mysql server with the command: sudo mysql
9. as shown below:

<img width="560" alt="Screen Shot 2022-09-03 at 11 11 54 AM" src="https://user-images.githubusercontent.com/112595648/188266043-edad2d54-591d-4063-8608-bf80c5c3904f.png">

10. I run the command below to remove the insecure default settings and change the password to PassWord.1 : ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '<img width="560" alt="Screen Shot 2022-09-03 at 11 11 54 AM" src="https://user-images.githubusercontent.com/112595648/188270123-54d7cc85-213d-48b4-9241-2d0f51738b7d.png">';

11. I Started the interractive script by running the command : sudo mysql_secure_installation

12 It requested for the password setted as below

<img width="560" alt="Screen Shot 2022-09-03 at 11 11 54 AM" src="https://user-images.githubusercontent.com/112595648/188269786-c461b4ef-3052-4dbf-bb3e-c1110cea586e.png">


13. Tested the login with the command: sudo mysql -p   the -p is because the root password is changed and will be promted for it

<img width="560" alt="Screen Shot 2022-09-03 at 11 11 54 AM" src="https://user-images.githubusercontent.com/112595648/188270158-f15f441b-1221-4b4a-a3e1-04414cb1b6d4.png">

14. Nxt we install all the packages needed for php to run with this command: sudo apt install php libapache2-mod-php php-mysql

15 i confirm the installtion with the command : php -v

<img width="566" alt="Screen Shot 2022-09-03 at 1 30 17 PM" src="https://user-images.githubusercontent.com/112595648/188270488-16dead42-7d43-4643-898c-31cc48b672c8.png">

16. now create a virtual host using the apache. setup a domain called projectlamp and we create a directory for it with the command : sudo mkdir /var/www/projectlamp

17. we assign the ownership of our current user with the directory with this command :  sudo chown -R $USER:$USER /var/www/projectlamp

18. Then, create and open a new configuration file in Apache’s sites-available directory using the VI command-line editor with the command : sudo vi /etc/apache2/sites-available/projectlamp.conf

19. then we insert and save the following comands: <VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

20. we use ls command to show the new file in the sites-available directory

<img width="565" alt="Screen Shot 2022-09-03 at 2 04 01 PM" src="https://user-images.githubusercontent.com/112595648/188271699-70ec66b7-2a7f-4275-b3f2-d80292c31b09.png">

21. use the command to enable the projectlamp created : sudo a2ensite projectlamp
22. disable the default site with the command : sudo a2dissite 000-default
23. check if the configurations has errors so far with the commnad : sudo apache2ctl configtest    as seen below everything looks ok

<img width="564" alt="Screen Shot 2022-09-03 at 2 07 22 PM" src="https://user-images.githubusercontent.com/112595648/188271837-9e124f3a-a01e-49a0-88e6-58f99c11444c.png">

24. we relaod apache with the command for the configs to take effect: sudo systemctl reload apache2
25. Create an index.html file in that location and use echo to write a text on the index.html create with echoe with the command : sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html

26. confirmed everything works well by entering the server public ip on the url
<img width="1138" alt="Screen Shot 2022-09-03 at 2 13 26 PM" src="https://user-images.githubusercontent.com/112595648/188272069-d542a5d9-f777-4875-8044-6c64878778b0.png">

27. next we enable php on the website and will change the directory index behaviour so that .php can load first over.html with this command : sudo vim /etc/apache2/mods-enabled/dir.conf
28. delete the content you have there with :%d and paste the script below: <IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
save with :wq

29. reload the apache with this command for the changes to take effect : sudo systemctl reload apache2
30. we create the index.php file as the new landing page with the command: vim /var/www/projectlamp/index.php

and save this content:
<?php
phpinfo();

31. for confirmation, enter the server address in the url again and this was the output as expected:

<img width="1346" alt="Screen Shot 2022-09-03 at 2 29 07 PM" src="https://user-images.githubusercontent.com/112595648/188273007-b63c7db9-f8eb-4bbd-a6ea-0072db4de1ab.png">


32. for security sake the page above should be removed because it contains so much information
sudo rm /var/www/projectlamp/index.php
