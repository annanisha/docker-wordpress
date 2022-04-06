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

Add ec-2 user to docker group

$ sudo usermod -a -G docker ec2-user
rep "docker" /etc/group
docker:x:992:ec2-user
