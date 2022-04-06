# docker-wordpress

## Descripton.

Docker is a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers.

Today, we are going to create a wordpress instance using docker.

## Steps to install wordpress using docker.

# Step 1: Install docker on your machine.

$ sudo yum install docker -y

Restart and enable service using following commands.

$ sudo systemctl restart docker.service
$ sudo systemctl enable docker.service

Add ec2-user to docker group

$ sudo usermod -a -G docker ec2-user
rep "docker" /etc/group
docker:x:992:ec2-user

# Step 2: Create mysql container.

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

# Step 3: Create wordpress container.

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
