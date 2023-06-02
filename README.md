# Host-a-wordpress-website-using-vpc-on-AWS

## Description 

Hosting a WordPress website using a Virtual Private Cloud (VPC) on AWS provides an enhanced level of security and control over your website's infrastructure. With a VPC, you can isolate your WordPress resources within a private network and have finer-grained control over inbound and outbound traffic.

### Step1:Create VPC with Public and Private Subnets

#### To create the VPC, go to the AWS console >In the VPC Dashboard> Create VPC

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/afa2880d-8975-46fe-a525-d3eb5ee338a4)

####  Click create VPC.

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/fd1b266b-9ebe-4efc-8166-64c29974b328)

#### Name the VPC . In the IPv4 cidr block space, type subnet as per requirment . Leave everything as default and scroll down and click create vpc.


![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/9b253417-4855-45d8-b5fb-b64c1246662f)

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/8f36413c-4b6c-4384-96c5-86bae3aecb8b)

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/94b99da2-b006-4cf9-9e2c-3f9d5994010e)

#### To eneble DNS hostname in the vpc,To do that, select "action" and then edit "vpc setting". In the next page that opens, check the enable "DNS hostname" box and scroll down and hit save button.

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/049dcd75-839d-45ee-b18e-b141f773be6a)

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/d398c1bb-bd85-4186-a33a-cfe7171582e3)

### Step2:Create Internet Gateway
#### On the vpc dashboard, click on internet gateway and hit create internet gateway.
![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/dd302599-b6ad-4fdb-9670-576dbdfaa93a)

#### Name it as per requirment, then scroll down and hit create internet gateway.

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/ac29c1b4-844f-47f7-a4dc-3a9734a94e2c)

### Step3: Attach the internet gateway
#### To the vpc that was created, to do that, click on "attach to a vpc" or "action". Under "available vpcs", select the VPC that was created,

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/5e33d84a-7349-41a2-afc8-73361136f845)

#### Select the VPC that was created, and click "attach internet gateway".

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/302dfa26-ea7f-47da-9f8b-2f2547a322d1)
![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/a1a907f2-2c5d-49e1-8f19-4577fefe9272)


### Step4:Create Subnets.

#### Now creating 3 subnets-2 public subnets and 1 private subnet
#### create a subnets in the first,second and third availability zones according to the vpc refference architecture. To do this, select "subnet" in the vpc dashboard and click "create subnets"

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/b4d45d87-acc1-438b-8d62-342d047b7ad3)

#### As per my requirement for first subet im using > under "vpc id", select vpc "my-dev-vpc" and the scroll down to subnet name "my-dev-vpc-public1",. Under "availability zone", select "us-east-2a". Under IPv4 Cidr block, type in "172.16.0.0/18". scroll down and click "create subnets"

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/e73a53a7-55bb-474b-9c64-bfc9d241cb78)
![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/683fe606-7b9a-476f-9759-4df55f349428)

####  As per my requirement for second subet im using > under "vpc id", select vpc "my-dev-vpc" and the scroll down to subnet name "my-dev-vpc-public2",. Under "availability zone", select "us-east-2b". Under IPv4 Cidr block, type in "172.16.64.0/18". scroll down and click "create subnets"

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/a44ca4ae-e52f-4e82-a357-eb64f74c93ad)

####  As per my requirement for third subet im using > under "vpc id", select vpc "my-dev-vpc" and the scroll down to subnet name "my-dev-vpc-private1",. Under "availability zone", select "us-east-2v". Under IPv4 Cidr block, type in "172.16.128.0/18". scroll down and click "create subnets"

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/e50f28ef-7a7c-4e33-87c5-e343ecb0e412)

### Step5: enable auto-assign ip for the subnet

#### To do this, select the first subnet and click "action", click "edit subnets settings", 

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/58a75ed6-ffb8-4a9b-9592-450dbdf34693)

####  under "auto-assign ip setting", enable "auto-assign public ipv4 address",click save.

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/140186f6-8ae7-4a82-8900-acb17d0826eb)

##### NOTE: Enable "auto-assign public ipv4 address" for 2nd public subnet also

### Step6:Create NAT Gateways in the Public Subnets

#### Select "natgateway" in the vpc dashboard and click "create nat gateways"

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/42cc734f-d7e0-438a-b2ce-69912502b9a3)

#### Give the name , select one of the public subnet,under "elastic ip allocation id", click "allocate elastic ip","create nat gateway".

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/128e0efe-45bd-4ee0-a7b3-71d99b02fdbf)
![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/3bb9453d-b392-490c-a040-4ba559de9625)

### Step 7: Edit default routing table of our vpc

#### Select the default route and in "Action" option choose "Edit routes"

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/3fc2e7ce-c912-4371-a71c-28befb91817a)

#### Then click "add route", under "destination", type in "0.0.0.0/0" in the box. After that, under "target", select "internet gateway", then click "save changes"

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/3c8db290-4b18-4530-bdb5-54edc793675a)

### Step 8: Create another route table for private subnet

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/b8725a8b-b509-4d76-9f42-9dc738c82b7f)

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/90c15ac6-d062-4ff9-9db6-e38f09b7efbd)

#### Next step add a route to the private route table to route traffic to the internet through the nat gateway in the public subnet .

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/b2dd4fe4-4701-4225-9574-35451460fe7e)

### Step 9: Subnet association

#####  Right click "edit subnet associations". , select private subnet click "save associations".

![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/2b19a9f6-27a8-4aa1-a8f8-c2348236fd17)
![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/08a8f3e7-7e6d-4819-97b4-46bf74350af8)

##### Note: By default all subnet will be associated with default route

### Step 10:Create Security Group

#### creating 3 security groups for 3 instance we are going to create.
              1>bastion sg
              2>frontend sg
              3>backend sg
              
 ##### NOTE:A bastion host is a special-purpose computer on a network specifically designed and configured to withstand attacks
 
 ##### 1:Security group for bastion,here im using sg name as "bastion sg"."Add inbound rule" as current ip of device and
 ##### "outboung rule" all traffic is allowed
 
 ###### NOTE:Select the vpc as we created 
 
 
 ![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/d45f7172-3386-477e-81a3-e76b8f8bd9cb)
![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/5479ffbe-8aac-4cde-99f8-ee7a15c7d6a6)
![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/10696be2-2d17-4eb9-bf9a-e56d6a4865c0)


 ##### 2:Security group for frondend ,here im using sg name as "frontend sg".Three "Add inbound rule">>ssh from "bastion security group id" ,http from "any 
 ##### ipv4",httpfrom "any ipv4"."Outboung rule">> all traffic is allowed
 
 ![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/7977b06c-8a7c-4fb8-ac4f-258f3223e778)
 
 ##### 3:Security group for backend ,here im using sg name as "frontend sg".Two "Add inbound rule">>ssh from "bastion security group id",
 #####  Allow "3306(mysql/aurora)" from "frontend-id"."Outboung rule">> all traffic is allowed
 
 ![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/87a13b41-a706-4259-b4e6-068f210343c5)
 
 ### Step 11: Launch the setup server (Ec2 instance)
 
 ##### Here we have to setup 3 instance
       1>bastion
       2>frondend
       3>backend
       
 ##### 1:bastion instance.
 ###### NOTE:Add name>>Select the created VPC>>Select one of the public subnet>>Select "existing security group" and add "bastion-sg" security group
 
 ![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/c5a48dc9-c205-4fd7-82e7-e3cf284b31f6)
 
 ##### 2:frondend instance.
 ###### NOTE:Add name>>Select the created VPC>>Select one of the public subnet>>Select "existing security group" and add "frondend-sg" security group
 
 ![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/86761023-3687-46a0-b716-2d9af4e50696)


  ##### 3:backend instance.
 ###### NOTE:Add name>>Select the created VPC>>Select one of the private subnet>>Select "existing security group" and add "backend-sg" security group
 
 ![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/3bc521bb-f8fd-4006-b5a2-c5ced818e0b5)

##### NOTE:We cannot directly ssh to "frontend" or "backend" server.We can only access "frontend" and "backend" through "bastion" server'
 
 ### Step 12: SSH to server
 
 ![image](https://github.com/Rashek-R/Host-a-wordpress-website-using-vpc-on-AWS/assets/134732001/bf1e18ba-bac2-475f-b33b-cd8cf23170ce)

#### Now from bastion server we can ssh to both frondend and backend server

### Step 13: Install database server in backend

#### install  "mariadb"

     >sudo yum install mariadb105-server -y
     >sudo systemctl restart mariadb.service
     >sudo systemctl enable mariadb.service

     >$ sudo netstat -ntlp

      >Active Internet connections (only servers)
      >Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
      >tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      2087/sshd: /usr/sbi 
      >tcp6       0      0 :::22                   :::*                    LISTEN      2087/sshd: /usr/sbi 
      >tcp6       0      0 :::3306                 :::*                    LISTEN      26214/mariadbd  
      
  #### install "mysql" 
  
       >sudo mysql_secure_installation 



NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.

Enter current password for root (enter for none): 
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.

       >Switch to unix_socket authentication [Y/n] n <<=========================
       >... skipping.

       >You already have your root account protected, so you can safely answer 'n'.

       >Change the root password? [Y/n] y
       >New password: 
       >Re-enter new password: 
       >Password updated successfully! 
       >Reloading privilege tables..
       >... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

       >Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

     >Disallow root login remotely? [Y/n] y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

      >Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

       >Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!

==========================

      >[ec2-user@ip-172-31-34-110 ~]$ mysql -u root -pmysqlroot123
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 11
Server version: 10.5.18-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

=========================


     >[ec2-user@ip-172-31-34-110 ~]$ mysql -u root -pmysqlroot123
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 11
Server version: 10.5.18-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

     >MariaDB [(none)]> create database blogdb;
      >Query OK, 1 row affected (0.000 sec)


       >MariaDB [(none)]> create user wpuser@'%' identified by 'wpuser123';
       >Query OK, 0 rows affected (0.001 sec)

       >MariaDB [(none)]> grant all privileges on blogdb.* to wpuser@'%';
       >Query OK, 0 rows affected (0.001 sec)

       >MariaDB [(none)]> flush privileges;
       >Query OK, 0 rows affected (0.001 sec)


       >[ec2-user@ip-172-31-34-110 ~]$ mysql -u wpuser -pwpuser123



       >MariaDB [(none)]> show databases;
       >+--------------------+
       >| Database           |
       >+--------------------+
       >| blogdb             |
       >| information_schema |
       >+--------------------+
       >2 rows in set (0.000 sec)




 
 
 
              
              




























