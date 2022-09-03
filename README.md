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

16. now create a virtual host using apache


