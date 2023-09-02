**WEB SOLUTION WITH WORDPRESS**

In this project we would be implementing a basic web solution called WORDPRESS while creating storage infrastructures on 2 Linux servers 

This project consists of two parts:

1) Configuration of storage systems focusing on working with disks, partitioning and creating volumes on Web and Data servers using the Linux Operating system 

2) Deployment of Web and Database tier of Web solutions by 

connecting WORDPRESS to a remote MySQL server 

It’s important to have web server installed separated with WordPress as the CLIENT while we install the database server separately this helps us in

separating the 2 servers just to enhance security and avoid natural disaster recovery in case of any unforeseen circumstance so as to void losing so much information.

#### Pre-requisite for the projects is the following. 

1) Fundamental Knowledge of Installing and downloading software 
1) Basic Understanding of Linux Commands 
1) AWS account login with 2 EC2 instances (Red Hat)
1) Webserver (WORDPRESS
1) Laptop or PC to serve as a client. 
1) Database Server (MYSQL database server)
1) Internet connection

## IMPLEMENTATION STEPS:

1) Ensure you login with your details to your AWS console via the  <https://aws.amazon.com>
1) Click on the EC2 link to create instances. 

![image](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/19ca370a-d38d-4582-b442-f32f12d49966)


iii)Click on launch instance dropdown button and select launch instance.

![image](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/f03e3637-73e9-4a78-986a-0790673d10bf)


Select Red-Hat from the quick start option and note that amazon machine image selection varies from user to user .Select red hat enterprise Linux 9 HVM SSD Volume type .

![image](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/c98fe2f2-732a-4141-9387-2e3e60ef2834)


Click on the “Create new key pair” link and ensure the Checkbox remains unchanged on the “Create security 

group”

![image](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/98b2c255-a962-4cf0-9bb1-3655fabf74a7)

![image](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/cced1ef5-e577-40ca-ae30-f52c7a1695c7)


Select 2 instances and Launch both instances 

![image](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/7cdb20b1-77d1-4048-be0c-7708f5cf51bd)


Instances are successfully launched as shown below

![image7](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/3bd1eee2-8209-45e9-bcaf-ebe0168ddbfb)



Then we name the 2 instance webserver and database respectively .

![Aspose Words 7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8 008](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/2bb10775-b6ed-482b-b998-ae6c30d47cb5)


![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.008.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.009.png)

The public  ip address of both servers are displayed below

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.010.jpeg)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.011.jpeg)

Click to connect to ssh 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.012.jpeg)

We then proceed to check the availability zone of our server and click add volumes.We are to create 3 volumes

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.013.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.014.png)

Select 10 Gib and the availability zone  and click to create volume

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.015.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.016.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.017.png)

After creating the 3 volumes we refresh and can see them below.We name them web1,web2,web3 respectively

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.018.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.019.png)

Then we now attach each of the 3 volumes to the webserver as seen below 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.020.jpeg)

All 3 attachments are seen below and are now ready for use 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.021.png)

**WEBSERVER CONFIGURATION**

Open git bash on visual studio code or whichever console is convenient to use. We are using git bash here with Visual Studio Code 

We rename the ip address as webserver as seen below

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.022.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.023.png)

Once all volumes have been attached you should run the lsblk command and you would be able to see all the 3 disks that have been created xvdf, xvdg and xvdh

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.024.png)

With the df -h command we can see the mount point available 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.025.png)

We have to create a partition on the physical disk. We use the gdisk function to create a single partition on xvdf, xvdg and xvdh.Please note all the devices are stored in /dev .

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.026.jpeg)We use the gdisk command as show below , Type “n” to add a new partition,

Choose 1 as the partition number and click enter button for the first and last sector .Enter :8300 for the default file system , 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.027.jpeg)

Type “p” to view the partition table. Use “w” to write the table and edit on the disk and type “w” and click enter and type “y” to proceed.Then it can be seen  that the operation was successful. 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.028.jpeg)

Repeat the same steps and create the partition for g and h partitions and the results are shown below

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.029.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.030.png)

Type lsblk command to check again and you would see that the xvdf1,xvdg1,xvdh1 files has been created .

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.031.png)

We then proceed to install the lvm2 package. 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.032.jpeg)

Next step is to create a physical volume using the pvcreate command for the xvdf1, xvdg1 and xvdh1 respectively

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.033.png)

We use the lsblk command to check the 3 physical volumes created 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.034.png)

Use the pvs command to check the 3 physical volumes.

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.035.png)

Volume groups is used to add together all physical volumes andmake them whole .We then use the vg-create command to let the 3 physical volume be seen as 1 logical volume and we name is webdata-vg as shown below

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.036.png)

Use “vgs” to check if it was implemented successfully. 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.037.png)

The reason the VSize is not 30g is because some little amount has been reserved for the disk itself if space are needed in the future 

From this volume group we can now create 2 logical volume which we give to our servers to use on apps and logs and confirm it was implemented successfully

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.038.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.039.png)

` `We can add 5g to the apps and logs by using this command for both of them as shown below  and make them 14 gig each .Check and confirm it was implemented successfully

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.040.jpeg)

Use pvs to check whats left of the gig size (1.99)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.041.png)

And format the 2 logical volumes (command apps and logs) with the mkfs  command

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.042.jpeg)

Next, we are creating a mount point for our devices but to create a directory called www. we need confirm it is not  existing already so we type the command below and we can confirm its not there and proceed to create the www directory

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.043.jpeg)

We can see the folder and file created .

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.044.jpeg)

We create another directory and folder (/home/recovery/logs) and mount the apps-lv device and place it on the directory (/var/www/html)

Please note that mounting means the data exist in both places .But you should always check the existing file to know its empty before performing the mount operation because it might lead to loss of data if you don’t check the file content .

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.045.png)

You can now proceed to mount and use the df -h command 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.046.png)

We have to check again for the logs file to investigate its content  before mounting .As you can see there are 496 files which could have been lost if we proceed by mounting which makes it very mandatory to check as they are very important 

to our machine .  

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.047.jpeg)

The solution to this is by copying the files in /var/log into  the /home/recovery/log file  and you can confirm it by simply checking its content as shown below

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.048.jpeg)

And with this you can see that the folder has been backed up 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.049.jpeg)

Proceed to mounting 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.050.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.051.png)

` `The command below shows that it has been properly mounted 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.052.png)

We should know that the mount is temporary and once the server is rebooted it would loose connection. We should ensure to make the connection persist and that would be by editing the fstab file and adding some crucial command to make it permanently stable

We check the blkid to check the commands we need to populate the fstab

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.053.jpeg)We are going to copy the UUID for the lv-apps and lv -logs and go back to our terminal.

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.054.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.055.png)

We have update the fstab and also reloaded the daemon 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.056.png)

**DATABASE SERVER PREPARATION**

In this preparation we would launch a red hat instance for the DB server and repeat all steps  and create a db-lv and mount It to a /db 

We would create volume and also take note of the availability zone of the database server and create 3 volumes

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.057.jpeg)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.058.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.059.jpeg)

Select 10 Gib and the availability zone  and click to create volume

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.060.jpeg)

Refresh to see all volumes created and name them db1,db2,db3 respectively and see they are available 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.061.png)Then we now attach each of the 3 volumes to the webserver as seen below 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.062.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.063.jpeg)

Repeat this steps for the rest of the volumes as seen below and all 3 volumes are now ready for use by the database server

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.064.png)

**DATABASE SERVER CONFIGURATION**

Open git bash on visual studio code or whichever console is convenient to use. We are using git bash here with Visual Studio Code 

We rename the ip address as webserver as seen below.

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.065.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.066.png)

Once all volumes have been attached you should run the lsblk command and you would be able to see all the 3 disks that have been created xvdf, xvdg and xvdh

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.067.png)

With the df -h command we can see the mount point available 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.068.png)

We use the gdisk command as show below , Type “n” to add a new partition,

Choose 1 as the partition number and click enter button for the first and last sector .Enter :8300 for the default file system , 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.069.jpeg)

Type “p” to view the partition table. Use “w” to write the table and edit on the disk and type “w” and click enter and type “y” to proceed. Then it can be seen  that the operation was successful. 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.070.jpeg)Type lsblk command to check again and you would see that the xvdf1,xvdg1,xvdh1 files has been created

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.071.png)

Repeat the same steps and create the partition for g and h partitions and the results are shown below

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.072.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.073.png)

We then proceed to install the lvm2 package. 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.074.jpeg)

Next step is to create a physical volume using the pvcreate command for the xvdf1, xvdg1 and xvdh1 respectively

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.075.png)

We use the lsblk command to check the 3 physical volumes created

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.076.png)

Use the pvs command to check the 3 physical volumes.

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.077.png)

Volume groups is used to add together all physical volumes and make them whole .We then use the vg-create command to let the 3 physical volume be seen as 1 logical volume and we name is database-vg as shown below

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.078.png)

Use “vgs” to check if it was implemented successfully. 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.079.png)

The reason the VSize is not 30g is because some little amount has been reserved for the disk itself if space is needed in the future 

From this volume group we can now create 2 logical volume which we give to our servers to use on apps and logs and confirm it was implemented successfully

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.080.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.081.png)

Use pvs to check what’s left of the gig size (9.99)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.082.png)

Next step is to create the mount point  .We create a directory called “db”

and create the file system using the mkfs command  and then mount 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.083.png)

We know we created the file but lets check to see if it has any content .As you can see below it has no content 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.084.png)

Then we mount it  and also confirm If it has been mounted with the  df -h command

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.085.png)

(Using blkid command )

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.086.png)

The next thing to do is to make sure that the connection is persisted and consistent even after reboot. We would be editing the /etc/fstab file to perform this action and confirm if success with the command below and have a system reload .Also check the df -h command to confirm its there  in the information provided 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.087.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.088.png)

Next step is to install word press on our webserver. 

**WORDPRESS INSTALLATION ON WEBSERVER**

This installation should be done in the webserver .We have to run an update on the webserver and the database server .

But before then we have to update both servers as shown below

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.089.jpeg)

We should check the security group of both instances to ensure they are all open to the traffic we want it to be.

We then proceed to install WordPress on our webserver. First ,Install wget,apache and its dependencies 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.090.jpeg)

Then we enable and start apache httpd 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.091.png)

Then we proceed to install the PHP and its dependencies 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.092.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.093.png)

We then proceed to list and reset and enable the PHP

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.094.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.095.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.096.jpeg)

Install other dependencies of php 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.097.png)

Start, enable and set Boolean value for Apache as shown below

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.098.png)

Restarting Apache 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.099.png)

Apache status and confirm there is no file on the /var/www/html location

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.100.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.101.png)

We proceed to create and change directory to WordPress and install it with its dependencies. 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.102.png)

Downloading in progress and finally completed .Configure selinux policies as well

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.103.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.104.png)

Go back to your database server to complete the installation and configuration.

Installing MySQL on database server, restart, enable and check status

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.105.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.106.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.107.png)

Configure DB to work with WordPress

We would create a database named wordpress and create my user  with your credentials and ensure you grant all permission and flush out privileges .Once done check the database tables and exit it 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.108.jpeg)

Please note that when we check the user  you would get this 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.109.png)

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.110.png)

We need to set the bind address :

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.111.png)

The next step would be to configure WORDPRESS which is the webserver to act as a client to connect to the remote database 

![](Aspose.Words.7bf68ce5-4ab0-4cd9-8b88-4d9aa92d06b8.112.png)
