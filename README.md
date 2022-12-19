# AWS-Docker

-- Update the installed packages and package cache on your instance.

sudo yum update -y

-- Install the most recent Docker Engine package.
sudo amazon-linux-extras install docker

-- Start the Docker service.
sudo service docker start

--Add the ec2-user to the docker group so you can execute Docker commands without using sudo
sudo usermod -a -G docker ec2-user


# INSTALL NGINX server through Docker file

# Pull the minimal Ubuntu image
FROM ubuntu

# Install Nginx
RUN apt-get -y update && apt-get -y install nginx

# Copy the Nginx config
COPY default /etc/nginx/sites-available/default

# Expose the port for access
EXPOSE 80/tcp

# Run the Nginx server
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]

#Install nginx server in Amazon linux2
$ sudo amazon-linux-extras list | grep nginx
 38  nginx1=latest            disabled      [ =stable ]

$ sudo amazon-linux-extras enable nginx1
 38  nginx1=latest            enabled      [ =stable ]
        
Now you can install:
$ sudo yum clean metadata
$ sudo yum -y install nginx
    
$ nginx -v
nginx version: nginx/1.16.1

# copy file from s3 to ec2 instance
1. Create an IAM role with S3 write access or admin access
2. Map the IAM role to an EC2 instance
3. Install AWS CLI in EC2 instance
4. Run the AWS s3 cp command to copy the files to the S3 bucket
# To List the S3 Bucket 
aws s3 ls s3://<S3bucketName>

# To copy the files from EC2 to S3
aws s3 cp <Fully Qualified Local filename> s3://<S3BucketName>




