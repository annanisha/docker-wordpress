# Docker-WordPress

## Description.

Docker is a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers.

Today, we are going to create a WordPress website using docker.

## Prerequisite.

Create an ec2 instance and install docker on it. 

This is not mandatory, you can also install docker on your local machine.

### Steps to install WordPress using docker.

### Step 1: Install docker on your machine.

$ sudo yum install docker -y

Restart and enable service using following commands.

$ sudo systemctl restart docker.service
$ sudo systemctl enable docker.service

Add ec2-user to docker group

$ sudo usermod -a -G docker ec2-user
grep "docker" /etc/group
docker:x:992:ec2-user

### Step 2: Create MySQL container.

docker container run \
-d \
--network wpnetwork \
--name database \
-e MYSQL_ROOT_PASSWORD="mysqlroot@123" \
-e MYSQL_DATABASE="wordpress" \
-e MYSQL_USER="wpuser" \
-e MYSQL_PASSWORD="wpuser@123" \
mysql:5.6

![mysql](https://user-images.githubusercontent.com/100779249/162000293-448dfc06-0c15-4052-a813-19a34a0d034f.png)

### Step 3: Create WordPress container.

 docker container run \
 -d \
 --name wordpress \
 --network wpnetwork \
 -p 80:80 \
 -e WORDPRESS_DB_HOST="database" \
 -e WORDPRESS_DB_USER="wpuser" \
 -e WORDPRESS_DB_PASSWORD="wpuser@123" \
 -e WORDPRESS_DB_NAME="wordpress" \
 wordpress:latest
 
 ![www](https://user-images.githubusercontent.com/100779249/162001017-bcc3759d-52f6-440a-8b0e-4930c18fc99d.png)
 
 ```
 [ec2-user@ip-172-31-46-9 ~]$ docker container ls
CONTAINER ID   IMAGE              COMMAND                  CREATED              STATUS              PORTS                               NAMES
f6b9fbbce3f7   wordpress:latest   "docker-entrypoint.s…"   3 seconds ago        Up 2 seconds        0.0.0.0:80->80/tcp, :::80->80/tcp   wordpress
55307a55d7ea   mysql:5.6          "docker-entrypoint.s…"   About a minute ago   Up About a minute   3306/tcp                            database
```

Now, call your website using ec2 public IP address and configure your WordPress website.

![sssssssssssss](https://user-images.githubusercontent.com/100779249/162004855-6d1d0e30-e60f-4092-9239-dbd4c8f036b6.png)

Wow!!! your WordPress website is live now!!

## Conclusion.

This article explains how to install WordPress using docker. Thank you!!
