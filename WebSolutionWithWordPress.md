# **WEB SOLUTION WITH WORDPRESS**

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

![image8](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/0c2a61e2-163a-4f50-8050-d886d4abab0c)

![image9](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/4a1f3670-cff9-41f7-af64-d32af9c065c5)

The public  ip address of both servers are displayed below

![image10](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/b4a176cb-8021-43b0-a7cc-01b70662210a)

![image11](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/43f315b7-8b35-436f-81c5-0fa3d54d40a6)

Click to connect to ssh 

![image12](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/62f4cdf5-a010-4ecb-a5b9-907e68cc4614)


We then proceed to check the availability zone of our server and click add volumes.We are to create 3 volumes

![image13](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/30dc83a7-fd9a-4975-aaf4-0f90cba57548)

![image14](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/09e27961-a264-4221-af60-73713d54972a)


Select 10 Gib and the availability zone  and click to create volume

![image15](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/f4cda03e-9b5a-487a-982e-8ac1e061683c)

![image16](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/430099b5-78ac-4063-bc2b-a6e905bb8991)

![image17](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/5d81902b-eec2-4130-b4d7-500b54c4d919)


After creating the 3 volumes we refresh and can see them below.We name them web1,web2,web3 respectively

![image18](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/e6eeeac3-7b24-4c1b-b4e8-6b4cef42a906)

![image19](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/d00295e5-f1da-4153-a772-843fe4330a13)


Then we now attach each of the 3 volumes to the webserver as seen below 

![image20](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/db66c795-621b-4fec-b174-5540b31c951c)


All 3 attachments are seen below and are now ready for use 

![image21](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/f9df83d6-c01a-42ad-8831-48376e48abf6)


**WEBSERVER CONFIGURATION**

Open git bash on visual studio code or whichever console is convenient to use. We are using git bash here with Visual Studio Code 

We rename the ip address as webserver as seen below

![image22](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/466debd5-e2f2-4dbe-b3ee-72ecf51ebbf4)

![image23](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/caf3c26d-7937-469a-8202-d67f8eaf0210)

Once all volumes have been attached you should run the lsblk command and you would be able to see all the 3 disks that have been created xvdf, xvdg and xvdh

![image24](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/a09eddb0-4585-4761-ba15-950cfa6a571c)

With the df -h command we can see the mount point available 

![image25](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/11c43697-2463-4437-99ff-094a02585218)


We have to create a partition on the physical disk. We use the gdisk function to create a single partition on xvdf, xvdg and xvdh.Please note all the devices are stored in /dev .

![image26](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/9cedda5d-4cc3-4af9-9725-728ca1f17c01)



We use the gdisk command as show below , Type “n” to add a new partition,

Choose 1 as the partition number and click enter button for the first and last sector .Enter :8300 for the default file system , 

![image27](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/2fd56516-b91b-4533-9fb7-0d91d926997f)


Type “p” to view the partition table. Use “w” to write the table and edit on the disk and type “w” and click enter and type “y” to proceed.Then it can be seen  that the operation was successful. 

![image28](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/5cdd2287-c97c-40f0-9578-bfbbe09b3782)


Repeat the same steps and create the partition for g and h partitions and the results are shown below

![image29](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/84c725ec-83c9-4569-a9e4-8a47c4df9428)

![image30](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/6151f75a-7281-4bfb-aff3-95e4697fd907)



Type lsblk command to check again and you would see that the xvdf1,xvdg1,xvdh1 files has been created .

![image31](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/bdd76394-1e15-4bb3-8b51-593e7e25661e)


We then proceed to install the lvm2 package. 

![image32](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/a65cd0d9-7bc7-4df4-9c95-ba32e3f40ee8)


Next step is to create a physical volume using the pvcreate command for the xvdf1, xvdg1 and xvdh1 respectively

![image33](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/7ecf070c-8e04-4b2a-bce8-ac0dbf69ef18)


We use the lsblk command to check the 3 physical volumes created 

![image34](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/454fe55a-797e-4a09-a8d2-089dce25de96)


Use the pvs command to check the 3 physical volumes.

![image35](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/174f39ce-fb57-422c-91bf-b774869d5c3d)


Volume groups is used to add together all physical volumes andmake them whole .We then use the vg-create command to let the 3 physical volume be seen as 1 logical volume and we name is webdata-vg as shown below

![image36](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/444feca1-4f24-4055-af11-579123719838)


Use “vgs” to check if it was implemented successfully. 

![image37](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/f9204abd-7fef-40cc-866d-71dacbdb702c)


The reason the VSize is not 30g is because some little amount has been reserved for the disk itself if space are needed in the future 

From this volume group we can now create 2 logical volume which we give to our servers to use on apps and logs and confirm it was implemented successfully

![image38](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/e8e0f90b-4e88-4236-a546-9d1a071d7154)

![image39](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/7a5fb5dd-14d6-40dc-b928-fc44b52c39ba)


` `We can add 5g to the apps and logs by using this command for both of them as shown below  and make them 14 gig each .Check and confirm it was implemented successfully

![image40](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/13ebb042-224f-4ecf-a187-2744864ddf94)


Use pvs to check whats left of the gig size (1.99)

![image41](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/02b22b4d-50d4-444a-bf9e-be8007213640)


And format the 2 logical volumes (command apps and logs) with the mkfs  command

![image42](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/b0d70350-bf3c-4392-95ec-3d8a642cfca9)


Next, we are creating a mount point for our devices but to create a directory called www. we need confirm it is not  existing already so we type the command below and we can confirm its not there and proceed to create the www directory

![image43](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/bc0f4ba4-e666-4213-a601-0798af542d31)


We can see the folder and file created .

![image44](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/be043970-9f39-4306-97fb-f3a41b704ef0)


We create another directory and folder (/home/recovery/logs) and mount the apps-lv device and place it on the directory (/var/www/html)

Please note that mounting means the data exist in both places .But you should always check the existing file to know its empty before performing the mount operation because it might lead to loss of data if you don’t check the file content .

![image45](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/46fbe8e4-32e3-41bb-b580-c0a91cc07a58)


You can now proceed to mount and use the df -h command 

![image46](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/68cdc12e-1f53-48ad-bd8e-c2ae53e43702)


We have to check again for the logs file to investigate its content  before mounting .As you can see there are 496 files which could have been lost if we proceed by mounting which makes it very mandatory to check as they are very important to our machine .  

![image47](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/fb49b222-537a-4f5b-b92f-39f1dde47df0)


The solution to this is by copying the files in /var/log into  the /home/recovery/log file  and you can confirm it by simply checking its content as shown below

![image48](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/ee8df8de-1e10-4943-b7d5-b2597134c7a7)


And with this you can see that the folder has been backed up 

![image49](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/7874d000-dcb8-433d-b205-95c7461f2d73)


Proceed to mounting 

![image50](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/81cb7dd7-3f4d-4f58-828c-2a3568d37a90)

![image51](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/05159491-07c9-43c4-8a22-9816e100d846)

` `The command below shows that it has been properly mounted 

![image52](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/28efee86-92c4-4478-995a-ec67b3bb565d)


We should know that the mount is temporary and once the server is rebooted it would loose connection. We should ensure to make the connection persist and that would be by editing the fstab file and adding some crucial command to make it permanently stable

We check the blkid to check the commands we need to populate the fstab

![image53](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/688178e4-ac3d-4843-a455-d9b234ef59d5)


We are going to copy the UUID for the lv-apps and lv -logs and go back to our terminal.

![image54](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/a283d94e-106e-4951-a40c-01fc6a2635c6)

![image55](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/979025af-5828-4463-b0ae-77a59da84610)


We have update the fstab and also reloaded the daemon 

![image56](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/19a996f7-cdfc-4b8c-aeb2-8c2f671ddd0d)


**DATABASE SERVER PREPARATION**

In this preparation we would launch a red hat instance for the DB server and repeat all steps  and create a db-lv and mount It to a /db 

We would create volume and also take note of the availability zone of the database server and create 3 volumes

![image57](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/f6f689f8-792d-4316-bc35-33b9b230e23c)

![image58](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/dc969191-4c30-4330-86d9-b7654583d4f5)

![image59](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/5d5f7c1c-7723-4847-aa5e-7b6cf50cfd5e)


Select 10 Gib and the availability zone  and click to create volume

![image60](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/da7f6177-1865-4372-8787-c2f3e2a66f2e)

Refresh to see all volumes created and name them db1,db2,db3 respectively and see they are available 

![image61](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/88e3f688-475c-4d64-b1e4-20aaedbff1eb)

Then we now attach each of the 3 volumes to the webserver as seen below 

![image62](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/adf5377c-a6f1-461d-a64d-779f6c0c704d)

![image63](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/d8fee7a8-063d-4128-9a20-47709b43c047)


Repeat this steps for the rest of the volumes as seen below and all 3 volumes are now ready for use by the database server

![image64](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/528643f7-1195-42b4-b94a-9d70bff208af)


**DATABASE SERVER CONFIGURATION**

Open git bash on visual studio code or whichever console is convenient to use. We are using git bash here with Visual Studio Code 

We rename the ip address as webserver as seen below.

![image65](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/e103509d-7e69-4e5c-9510-cc6598731c5c)

![image66](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/36cfc062-ec4f-4cf0-b7c7-e8e4f26a645c)


Once all volumes have been attached you should run the lsblk command and you would be able to see all the 3 disks that have been created xvdf, xvdg and xvdh

![image67](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/3cd093dd-ad42-4a87-a49f-cdfca34de0de)


With the df -h command we can see the mount point available 

![image68](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/73f1705b-b25e-426b-8dab-29b3950e3935)


We use the gdisk command as show below , Type “n” to add a new partition,

Choose 1 as the partition number and click enter button for the first and last sector .Enter :8300 for the default file system , 

![image69](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/3ee118e4-c7d4-468e-9441-28854200b93f)


Type “p” to view the partition table. Use “w” to write the table and edit on the disk and type “w” and click enter and type “y” to proceed. Then it can be seen  that the operation was successful. 

![image70](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/8010611c-f910-4ab8-8297-0743715d019f)

Type lsblk command to check again and you would see that the xvdf1,xvdg1,xvdh1 files has been created

![image71](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/b2e6c3cd-301f-4773-b390-a7572202f91c)


Repeat the same steps and create the partition for g and h partitions and the results are shown below

![image72](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/87a3e2f9-486b-4ab7-8143-7e2b94df1aab)

![image73](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/ea5aa0bd-eba5-4129-943b-e0df7f37ba16)

We then proceed to install the lvm2 package. 

![image74](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/c11f4042-0d4f-447f-a4a9-630909e7186c)


Next step is to create a physical volume using the pvcreate command for the xvdf1, xvdg1 and xvdh1 respectively

![image75](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/4c85fa4f-9f69-4263-8055-bc97a52de9bd)


We use the lsblk command to check the 3 physical volumes created

![image76](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/7e3ef4c7-207b-49d9-be68-a15bdfc7365b)


Use the pvs command to check the 3 physical volumes.

![image77](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/49b22f8c-d869-4704-8265-138d6f78ed61)


Volume groups is used to add together all physical volumes and make them whole .We then use the vg-create command to let the 3 physical volume be seen as 1 logical volume and we name is database-vg as shown below

![image78](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/f87ca2f3-1157-4c20-8e3e-e9e89f35b734)


Use “vgs” to check if it was implemented successfully. 

![image79](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/ed3c5651-d0d0-494d-a3c9-b086d8da78b0)


The reason the VSize is not 30g is because some little amount has been reserved for the disk itself if space is needed in the future 

From this volume group we can now create 2 logical volume which we give to our servers to use on apps and logs and confirm it was implemented successfully

![image80](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/84e0080e-5a08-4012-b53b-4d4209c8e476)


![image81](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/a88d442d-b85b-4eed-9a11-92b582cf9490)


Use pvs to check what’s left of the gig size (9.99)

![image82](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/8d9c9131-d2aa-46c1-8eaf-fab89f4935bd)


Next step is to create the mount point  .We create a directory called “db”  and create the file system using the mkfs command  and then mount 

![image83](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/bbc6bbf1-c2f7-4521-9752-037338672ed7)


We know we created the file but lets check to see if it has any content .As you can see below it has no content 

![image84](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/6d9743e5-09d0-4cee-b181-878c12e99bbc)


Then we mount it  and also confirm If it has been mounted with the  df -h command

![image85](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/4c966590-96f9-4b3a-a015-24458fb36741)

(Using blkid command )

![image86](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/34a9c29d-ce6f-491d-b362-44dcde4c3545)


Proceed to make sure that the connection is persisted and consistent even after reboot. We would be editing the /etc/fstab file to perform this action and confirm if success with the command below and have a system reload .Also check the df -h command to confirm its there  in the information provided 


![image87](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/63d851b1-2f43-4df0-a12f-218c98c727ca)

![image88](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/871626db-eb40-4426-923c-9e22456af632)


Next step is to install word press on our webserver. 

**WORDPRESS INSTALLATION ON WEBSERVER**

This installation should be done in the webserver .We have to run an update on the webserver and the database server .

But before then we have to update both servers as shown below

![image89](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/b4415f58-ebd8-42b7-bfbe-1e5b0fec0b7e)


We should check the security group of both instances to ensure they are all open to the traffic we want it to be.

We then proceed to install WordPress on our webserver. First ,Install wget,apache and its dependencies 

![image90](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/1df2d692-bb2b-4619-817c-efbc6ea5cd95)


Then we enable and start apache httpd 

![image91](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/46160f71-fc21-44b8-a5e6-71500b662a40)


Then we proceed to install the PHP and its dependencies 

![image92](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/3c82c424-33b2-48da-8bf9-425ed3cdc3c3)

![image93](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/0b428121-f068-4d73-aaf4-2e1e96a8d7f5)

We then proceed to list and reset and enable the PHP

![image94](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/e24f80e6-fc43-4f9d-bea5-863d806d6af0)

![image95](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/f9bc94b7-94a8-4934-ab68-c7a82567fffd)

![image96](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/66ffbc21-c045-48ba-adf4-77a109fefe9e)


Start, enable and set Boolean value for Apache as shown below

![image97](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/d4a279e4-fc00-4664-b6a9-02cb91be85f4)

![image98](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/7efbaabd-65c9-45d9-93c7-eb35c8b924dd)

Restarting Apache 

![image99](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/8d172330-3031-4b67-9ec4-fb270532e551)


Apache status and confirm there is no file on the /var/www/html location

![image100](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/84b40a5f-700e-49a4-b13c-6290a9c26da7)

![image101](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/27a47718-6465-45d3-9cbf-a7f79ad12cd1)

We proceed to create and change directory to WordPress and install it with its dependencies. 

![image102](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/c5a43661-be0d-4c07-8beb-6dc35491cd35)

Downloading in progress and finally completed .Configure selinux policies as well

![image103](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/341d9053-a2a0-4cbc-8a0d-070da4e5ed89)

![image104](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/d60a57bf-25a1-4a03-be2f-1203215c1b84)

Go back to your database server to complete the installation and configuration.

Installing MySQL on database server, restart, enable and check status

![image105](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/bd34e88b-3d9d-4a5f-a82e-d006662322d0)

![image106](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/cc0731b8-8ee4-463e-9aa9-cdc369a5cd72)

![image107](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/c3d4aafc-5a0e-4787-9866-f005533b2880)


Configure DB to work with WordPress

We would create a database named wordpress and create my user  with your credentials and ensure you grant all permission and flush out privileges .Once done check the database tables and exit it .

![image108](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/bf1ff8be-2e40-41e7-88eb-45169433abe8)

Please note that when we check the user  you would get this 

![image109](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/b4ab02cf-2219-43fb-b3da-eda5e469e45d)

![image110](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/3d01a7c1-9d08-4b64-aa6c-6bc960abe9ce)

We need to set the bind address :

![image111](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/888bd6d2-be0a-4739-bd3d-2a7c7c525f60)


The next step would be to configure WORDPRESS which is the webserver to act as a client to connect to the remote database 

![image112](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/52d02b00-19a0-41a1-8331-7a04761d3f8e)

Launch on the browser 
![website](https://github.com/eyewande2022/DevOpsDeploy/assets/116227096/271b2e95-ca01-4317-b2d6-d235a7d23df6)


