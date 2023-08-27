
# DEPLOYMENT OF A FULLY FUNCTIONAL MY-SQL CLIENT/SERVER ARCHITECTURE


## Client-Server Architecture

Client-Server Architecture involves the connecting together of one or more computers through a network to send and receive request between one another .This type of architecture involves each machine taking up the roles of a CLIENT  who continually sends a request and the other machine receives and responds to the request sent which is known as a SERVER .

In this project we would be working with the following:

A webserver that serves a client role connects and communicates back and forth with a database server whom in turn receives and respond to the webserver.

#### Pre-requisite for the project is the following.

1) Fundamental Knowledge of Installing and downloading software 
1) Basic Understanding of Linux Commands 
1) AWS account login with EC2 instance 
1) Internet connection

#### Implementation Steps:

1) Ensure you login with your details to your AWS console via the <https://aws.amazon.com>
  
1) Click on the EC2 link to create 2 instances namely MySQL server and MySQL client.

![image1](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/17d8561c-3d9e-4682-9825-265c83d139be)


The 2 instances successfully launched and click to view Instance details with the IP address. Please note by default both instances were created in the same local virtual network, hence they would communicate on the same IP address. 

![image2](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/ff90c432-94ce-4c49-8877-fd51a9e29880)


Click the “Connect” button and copy the ssh client details we would be using on the git bash console.

![image3](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/706a7402-faef-43e7-b26e-4367b3b0424c)

Click on security button and then proceed to click the security  group link.

![image4](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/9ee1e1ef-c50c-46ab-a00a-b01a63188fd2)

![image5](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/914497b5-4070-4272-bce4-5005ebd6127d)

Proceed to editing the inbound rules to add and save rules. Ensure you allocate port 3306 on MYSQL server with the ip address shown below. Always make sure the Ip address is only accessible by the MySQL client server 


![image6](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/9f577f42-6db3-49d0-9cd7-63f4616b5b7a)

![image7](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/cf1bcffe-5a20-480a-8b44-bf0075a13633)

![image8](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/8de2ca7a-9820-4b47-a3f7-0642897dcc93)

#### Rules added.

![image9](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/5e014559-883a-41bc-b1e4-a0b55d943845)

Open git bash on visual studio code or whichever console is convenient to use. We are using git bash here with Visual Studio Code. Type YES to connect.

![image10](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/403714c0-1114-42b6-9a84-c530b85a3a23)

Proceed to updating the lists of packages in the package manager.

![image11](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/13f1cf81-957e-407f-8239-92b0401ecbd1)

Then we proceed to install MySQL server

![image12](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/6d313d12-d452-40fa-85f6-b10136558078)

We enable the MySQL server and then proceed to secure the  server using a blank password.


![image13](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/889df33a-8a8c-47c8-a23e-967d2d3c2ed9)

After this we connect back to our MySQL database server to  create a data base ,grant all permission for the user created  and finally flush privileges and quit the MySQL

![image14](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/cf09b488-aecd-4eaa-b5dd-f695e14aeaf0)


We would need to configure MySQL server to allow connection  to remote host as shown below by editing the .cnf file and  change the bind address to 0.0.0.0 as seen below

![image15](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/4533abf3-bed2-4602-9f75-5f45c05cffe0)

![image16](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/cd1a0d18-fd27-4c41-b38e-cb24dc866787)


#### CONFIGURATION OF MYSQL – CLIENT

Then we go back to AWS to connect the MYSQL -client server

Click the “Connect” button and copy the ssh client details we would be using on the git bash console.

![image17](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/42f9f877-645d-4279-925d-be7b7068e47a)

Click on security button and then proceed to click the security group link.

![image18](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/2f3bfd74-2e6c-449b-97fe-12dbd350d73d)

![image19](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/0add0b4b-bb40-4d05-b070-e51ce644aa2d)

Proceed to editing the inbound rules to add and save rules.Ensure you allocate port 3306 on MYSQL server with the ip address shown below .Always make sure the Ip address is only accessible by the MySQL client server

![image20](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/610b22c9-6b75-47a4-9aa6-00855cf4d9ea)

![image21](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/04833fba-0351-4b3f-b23e-1a821e9a4e75)

![image22](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/c9d2672f-3f4d-4800-b066-0add40a0a167)

![image23](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/00376d96-9616-405a-a61c-d460f16d19a9)


#### Rules added

![image24](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/d4c2e4fd-0720-432c-a94b-8aaf3870e6c0)

Open git bash on visual studio code or whichever console is convenient to use. We are using git bash here with Visual Studio Code. Type YES to connect.


![image25](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/3fb388cb-471d-4d6c-b886-b7c69fcc18ce)

Proceed to updating the lists of packages in the package manager.

![image26](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/c7dc6698-b896-4643-9b29-8da661ff7528)

Then we proceed to install MySQL client and confirm the initial Ip address on the server

![image27](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/3f139cb3-1ed0-4f68-91e2-614e7fee5c84)

![image28](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/bb1f550b-0418-4d20-97b8-922e4713e321)

We then connect with the command below to the remote  database server.

![image29](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/609d2494-f988-4757-bad3-499cc2d85f30)

Then we confirm by showing the databases as shown below.

![image30](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/99167ea4-c560-4bcf-9564-a8592bb7530a)

This shows that we have successfully deployed a fully  functional My-SQL Client-Server set up.
