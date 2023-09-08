# **DEVOPS TOOLING WEBSITE SOLUTION**

A DevOps team utilizes various tooling solutions in order to help the
team carry out their day-to day activities in managing, developing,
testing, deploying and monitoring different projects .

In this project we would be implementing a DevOps solution that consist
of the following components

## Pre-requisite for the projects is the following.

1\) Fundamental Knowledge of Installing and downloading software\
2) Basic Understanding of Linux Commands\
3) AWS account login with EC2 instances\
4) Webserver Linux: Red Hat Enterprise Linux 9\
5) Database Server: On Ubuntu 22.04+ MySQL\
6) Storage Server: Red Hat Enterprise Linux 9 +NFS Server 
7) Programming Language: PHP\
8) Code Repository\
9) Internet connection

## IMPLEMENTATION STEPS: Set up of all EC-2 instances.

i) Ensure you login with your details to your AWS console via the\
ii) Click on the EC2 link and spin up 5 EC2 instances and make sure they are set up with the operating systems below 
4 Red Hat Enterprise Linux 9 Operating system (free tier) comprising of One NFS server and 3 webservers .You can see the instance state
that shows all 5 servers are currently running . The names are


NFS Server , WebServer1, WebServer2, WebServer3

![image1](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/7912a6b2-e61b-498f-9bfc-cfea5ea9146f)

1 Ubuntu Operating system comprising of the Database server. The name is DATABASE-SERVERUB

![image2](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/0e359559-9eba-4726-a34f-964737bbb0fa)


Then we proceed to configuring the NFS Server

## **NFS SERVER CONFIGURATION**

We open git bash on visual studio code or whichever console is
convenient to use. We are using git bash here with Visual Studio Code.
We are connecting the ssh and typing yes and once the connection is
successful, we proceed to naming the nfs server. This is so that we can
be able to distinct each server by their names and avoid confusion with
other server we would be configuring .The server name was edited as
shown below

![image3](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/12d6e8bf-f245-4879-8ba5-10a3b69a4b2f)


This is also done in the webserver1 and 2 as seen below.

![image4](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/432d252c-8ab2-4881-90ce-db1e1fbd788f)


![image5](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/3998e1d8-8287-45a3-9da1-bf38123cc0d1)


The next step would be to go back to the AWS console click to create the volumes. You must also check the availability zones as they play a
crucial role in the location in which the volumes are created. Ensure the sizes are 10 gig and create volume as seen below.

![image6](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/5896eb65-b313-4d7e-8c5c-2d41e406f434)


![image7](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/541243c0-de3b-4674-8d6b-4116618caee7)


![image8](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/5c22ecab-c2b3-472a-afee-e254b59c54a0)

![image9](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/3cd7746b-30e8-436e-908c-0dabb911c411)


Repeat the same steps for the other 2 volumes.Navigate to the volume created, Chose the instance you are attaching to (NFS SERVER ) and attach volumes and start using them .

![image10](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/78fc7cef-83f2-4ba7-a562-c72c4acc37b4)


Navigate back to the terminal and type the lsblk command to see the EBS volumes we attached. Usese the command below to
partition the drive and use the help command to see the options available to add a new partition.

![image11](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/ffd11511-9ca6-49bb-b3f1-06ef24958019)


Type "n" to add a new partition,
Choose 1 as the partition number
Click enter button for the first and last sector .
Enter :8300 for the default file system as shown below

![image12](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/cb82e112-2102-4008-8d27-63e5218e15e7)


You can type "p" to view the partition table as shown below.

![image13](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/973fafca-a162-43a1-bf6f-74306febc082)


We use "w" to write the table and edit on the disk 
Type "w" and click enter
Type "y" to proceed.

![image14](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/df81bcd4-b03a-47d9-a95a-a70df6771b95)


Itstates that the operation was successful.

![image15](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/1e5a51e0-00cb-40ee-8952-3e2e01b69574)


Type lsblk command to check again and you would see that the xvdf file now has where the partition was created as seen below

![image16](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/cee9be1c-d383-4a42-8471-0ebdfb8c464b)


Repeat the same steps and create the partition for " g and h " partitions and the results are shown below

![image17](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/10390808-ba59-42ad-88d5-cd3a5412d4bb)

![image18](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/bef1d4cf-cf10-478b-98a1-2d2d606da932)


Proceed to install the lvm2 package.

![image19](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/89bee972-02df-4615-9eb7-2d7ffa43e6fd)


After that is successfully installed, we use the lsblk command to check our 3 partitions created

![image20](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/bfd7dcd7-1124-421c-94dc-884a81f435c4)


Create a physical volume using the pvcreate  command for the xvdf1, xvdg1 and xvdh1  respectively

![image21](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/d46e4ac1-5a4e-4ab0-99cf-d8b5537f873a)


Use the lsblk command to check the 3 physical volumes created

![image22](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/abe70b6a-ab20-44d7-bff0-3ad6cc1922b5)


Use the pvs command to check the 3 physical volumes.

![image23](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/de52e7ea-b929-43da-ad94-f757a67593e9)


We then use the vg-create command to let the 3 physical volume be seen as 1 logical volume and we name is webdata-vg as shown below

![image24](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/10c0a432-047d-4337-93cb-c97f85faa120)


Use "vgs" to check if it was implemented successfully.

![image25](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/4da3ab0b-f57d-4da7-a9da-14f62198cff9)


Next step would be to create 3 logical volumes apps, logs and opt as shown below and confirm it was implemented successfully

![image26](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/38322d34-87d2-45d3-bd3f-2067d69db5f8)


Using the lsblk command to view all we have done since starting the partition creation, we can see the full detailed structure created as shown below

![image27](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/c668d5ef-ca2a-4a48-8acf-ba92d70bedc3)


We need to format the extra metadata that came along with this volume with the mkfs command below.

First, we check the devices using the /dev command

![image28](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/c3217ef7-bc66-4d74-a8fe-150b589e29d7)


And format the 3 logical volume (command apps, logs and opt) with the mkfs command

![image29](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/b2bdebda-e24d-4450-9372-dcaf30510cd9)


While in the NFS server we are to create some mount point on the mount directory on the logical volumes. We create the 3 directories as shown
below and check it was created successfully.

![image30](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/5b2aceb3-e858-4c41-9e6b-4db0337d59fc)


We would then mount the 3 logical volume path with the 3 mounting points as shown below

![image31](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/0fb4165d-8fb9-49e5-9e96-1613bcbb190e)


The next step would be to install the NFS server. Please take note that this is the place we store all the data and by storing it ,the webserver
automatically becomes the NFS client.

The installation of the NFS SERVER is done with the commands below

![image32](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/86342b45-a22d-43d3-a19f-36e1edb9c819)

NFS server installation completed, enabled and actively running.

![image33](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/3750aa40-1325-4f3e-aab5-f0facd090041)

Press q to quit and get back on the terminal

The next step would be to export the mount for webservers from subnet
cidr. Click on networking button and then proceed to click the subnet ID
link as shown below.

![image34](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/9b29c900-55c7-422d-b1eb-52c9101296c4)


![image35](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/7fb7de70-3b04-4b24-aedd-d320117c9adc)


The ipv4 cidr is shown below

![image36](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/1598a69d-ad00-47cb-aeed-3292497b8643)


Please note: The lower the number of cidr the higher the number of computers that can gain access to that server .This can
connect 4096 computers and shows the importance of cidr. Copy the cidr for future use.

We then navigate back to give permissions to allow our webservers access to read, write and execute .We can give permission to root or simply say
nobody . In this case we would say nobody because we want everyone to have access to it and it is not own by anyone.

Before the permission was changed

![image37](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/2c43b341-76ea-459c-94ca-b73eaaea0642)

After permission was allowed. see below as permission has been granted to nobody as well as the chmod 777 permission.

![image38](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/90116300-b9e3-4d5c-a3ec-56898c95b903)


We would then proceed to restart our NFS server after mounting of the logical volumes.

We then proceed to configure access to NFS from our clients within the same subnet ipv4 cidr as shown below.

![image39](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/96f7df6a-4bbe-4dcf-b1b9-a0b46d076d55)


Paste the code below in /etc/exports, Save and quit to get back to the terminal

![image40](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/a3ac46d1-11d2-4356-b9bb-2322968aba1b)


Verify they are properly mounted successfully with the command below.

![image41](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/76bd095a-f522-4d47-bc97-b8b8535472d2)


The next process is to go back to AWS security group for NFS server to open the ports tcp and udp via the inbound rules

![image42](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/0d63aa94-5ac7-4f4a-a730-54f23b7015ca)


Click security and security group

![image43](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/7d99191d-5294-43bf-8386-b5c9450afd25)


Add all rules.

![image44](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/50852d2f-9fb2-412a-9df3-2bd3582ddbbb)


Including the subnet cidr block of the webservers to access the NFS server.

![image45](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/e92fd79e-60a0-4a49-a77c-475bd97848b4)


Added successfully

![image46](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/c0e5070c-6dee-4c56-8efc-d5219b950731)


Now we proceed to the next stage to configure the database server.

## **DATABASE SERVER CONFIGURATION**

To configure our database server, we would install MySQL server and also created an hostname for the ip address for easy use.

![image47](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/ae1485db-41c9-41b6-942d-5d7b623fe880)


To access the MySQL environment, we use the command below

![image48](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/27a9d4cd-8e5b-4e76-af8d-72c015f72cfc)

but when we exit out of it, we need to use this

![image49](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/07dec52e-03a4-4899-9092-da754d7d7272)


The next thing would be to create a database. Lets show the current state of the database and it is as shown as below

![image50](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/8b54c85f-50e4-4d36-bdf3-dee5647168cc)


To use and show all tables in the MySQL ,

![image51](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/098f2c8e-000d-4164-9fed-abb72a098b82)


We would be creating the following and ensuring the ipv4 cidr   is included when creating the database server.

i)Database name: tooling     ii) Database username: webaccess

We would be using authentication by granting all privileges to webaccess from tooling including all tables in it.

![image52](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/102777c8-7ac7-4353-89e9-12cc25dd37ea)


Now lets proceed by flushing the privileges and show the database to see if we successfully created the databases.

![image53](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/105d2ab9-69bd-4143-ae59-7e47ac57db04)


Type: "Use tooling" to activate the database and show tables

![image54](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/dac7cdbc-5a78-4e3a-8dfc-86af8c5525c5)

![image55](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/9c31b01e-f56f-435e-8bc6-bf9cfa18788a)


The new user called webaccess is shown below.

![image56](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/b1d650f4-3906-4104-807b-4f3e66715a01)


Now we navigate back to the webservers.

## **WEBSERVERS**

We would be working on the 3 webservers but also note that they would
also represent as an NFS client to our NFS server when it stores
information. We intend to display the web page on the webserver. We want
to be able to read and write on the web page and we intend to gain
access to /var/www to retrieve the html

We would proceed with the first step by configuring the NFS CLIENTS on
all 3 servers.

We have to update the package manager

![image57](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/4dd36255-6af9-4238-8d10-65783dfa6625)


And install nfs-util

![image58](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/e24e635a-3527-4749-a6a5-84f103d80b1a)


Then we must create the /var/www directory and then mount the path where we would be installing the APACHE server (httpd).

Mounting is where we would be doing the connection linking the NFS CLIENT (Webserver)and the NFS server

We should check the hard disk df -h command to check how much disk available on the computer.

![image59](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/a3b3208f-b516-427c-bb58-310469a05f08)


To confirm if the mounting was successful we can try an experiment by changing directory to /var/www , and checking its content which should 
be blank, proceed to create a file name testfile .

![image60](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/0d6e5220-9750-4a6e-8bee-8fb974fd4a1c)


Navigate back to NFS server. Change directory to /mnt and check its content. You would find the file testfile there .

![image61](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/fc1db0dd-3c8a-4802-bc0b-17cbb26a94c7)


This confirms that our NFS CLIENT has been successfully connected to store information on the NFS SERVER .

Please note that when you reboot this server it would not retain the connecting state and connection would be lost but to make it connect
constantly we need to modify the fstab file .

![image62](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/1971b74b-ce7b-4b1c-a323-c0bd7ed2129f)


![image63](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/02ab13e7-a7be-49fc-8bdd-f113bc63916e)


Proceed to install Apache and PHP from a third party Remi's repository shown below

![image64](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/728cf04b-e3eb-47e2-a3cc-dcac3c51a4ae)

Install Apache

![image62](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/311d0802-a6a9-4afb-ad32-68982b06cb1e)


Installation continued and type y
![image65](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/9b395ae6-5a4f-4aef-991e-e84f6559092a)



![image66](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/2dd72546-bdf9-4f99-b169-d78d58e0e0cb)



All our packages are installed then we check if PHP is available on our repository version 8.1 which is a better upgrade\
compare to 7.4


![image67](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/81a3f6c4-4eec-4f49-a41b-1c5f0a3a4b4a)

You can still run the command without the: remi-7.4 to get the installation and click yes

![image68](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/bf2499a2-0bf4-4887-bfc6-2f40e821d7ab)


![image69](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/96c301d4-3084-40c8-89b3-18526a533025)

Then we proceed to install the PHP and type y and click enter

![image70](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/c4fa465f-f0d1-4b69-baeb-e0493cee4976)


![image69](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/410ddfa1-0b2c-4858-acb1-3238b0ea930b)


We then proceed to start PHP and enable it and then check the status to know if it is running .This can be seen below

![image71](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/eae86ca7-8dca-4b8f-b1bb-cd7b8fd9ba06)


Next is to set a Boolean and ensure that port 80 is opened.

![image72](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/383e61f0-0657-40eb-9007-751a736343fb)


Run the mount command and check the df -h command below

![image73](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/b66b0752-3caf-4c8b-a84a-8bc6468672a4)

You can now start the httpd and check status as well.

![image74](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/8619f4e4-ec5f-4c41-b6cb-fc6c4159fe94)


Enable the httpd

![image75](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/828ea295-c3fe-4551-893c-9bbe2907eb62)

We can check the webserver and copy the public Ip address.

![image76](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/4cbfde53-d0ea-4ce2-b8cb-320599924cfb)


We have been able to configure the server successfully.

We have to locate the log folder for apache httpd on the webserver.Change directory to /var/log and check its content, then you can change
directory to httpd

![image77](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/dc3dac18-69ca-47f7-b6ab-3b7869bcd2b4)


Please note if all troubleshooting fails, always remember selinux to help you out in terms of permission

Run the mount command and check the df -h command below

We should make sure we mount the /mnt/logs on /var/log/httpd and add  this file to the fstab. This is important for rebooting as well to keep
the connection available at all times making sure there is persistence.

See below

![2023-09-08 07_24_55-DevOpsToolingWebsiteSolution pdf and 5 more pages - Personal - Microsoft​ Edge](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/e9477e0b-a4c2-4039-b831-78a8e19ef5ef)


![image78](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/91a1325d-d326-4ac3-af97-de56a827985c)


![image79](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/af552192-94af-4032-916a-eb6974847bd0)


We now proceed create a fork a repository to retrieve the source code
from the git hub account.

First install git on the webserver

![image80](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/bdc36a8a-4e4c-40a9-aa49-7e6088e710ad)


Once installed then you clone the https repo.

![image81](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/a14c2c83-21ca-4aa9-b489-cc6518ef2ec4)


Then you proceed to deploying the website code into the webserver. Change directory into tooling and check its contents.

Then we should copy all files in the tooling directory into the  var/www/html file.

From the tooling directory, Change directory to var/www/html and view the content to the see copied files from tooling shown below.

![image82](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/5de9e1e2-c993-4462-83bb-819a68cad26d)


From the html directory change directory into /etc/httpd/conf.d and use the cat command to view the welcome.conf file .

![image83](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/ebb20ada-0106-42ae-be87-6ddd2cb5b7c2)


We would now edit the functions.php file in the html folder.

![image84](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/be5af54b-2d92-450f-a72c-a34834b859c9)


This helps us connect the application to the database. We insert the database private ip, database username ,password and database name as
shown below. Please note this only needs to be configured on one of the server and then its connected.

![image85](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/35d5d95b-f310-49b9-931f-a7d6ed1eebd1)


Then we proceed by applying the tooling-db.sql script to our data base using the command below. When entering the data we can only put the
database private ip ,database username and database name but not the password as it is confidential ,so we would leave it blank and would be
executed. We are going to install MySQL client because the action would be taking place on the webserver

![image86](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/73a4930f-55ab-4095-a74a-9a025cd87572)


So, we proceed by writing the command

![image87](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/be95d4a8-0b03-4ab5-843f-f963ab2796e0)


Check blkid to view the id .



![image88](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/62aa72e9-1d5f-4660-a32a-a6ba0f4ca3c8)

![image87](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/e2b79862-4aa4-49d8-90e4-87063a26b5cc)

Then we launch out ip addresses for the 2 server and it is

successfully displayed

![image89](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/4aa6531d-a1dc-49ee-b95a-c41216482090)


![image90](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/48f76220-a0ac-4ef0-9a65-547c64aea1e8)


We would go further to type in the details for the username and password
and they both are successfully logged

![image91](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/0f5c3bde-df43-4bfe-a2c7-c57cc936e684)


![image92](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/1b0caa20-4612-418f-8499-c9f2386513a9)


Finally, we have successfully implemented a web solution using LAMP
stack with remote databases and NFS Servers.
