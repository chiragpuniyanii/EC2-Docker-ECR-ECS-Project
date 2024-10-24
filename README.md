# EC2-Docker-ECR-ECS-Project

This project automates the deployment of a Dockerized Apache web server on AWS EC2. It covers the setup of Elastic Container Registry (ECR), Elastic Container Service (ECS) cluster, and a load balancer to manage incoming traffic.

## Project Overview

This guide walks through the complete process of deploying a web application using Docker containers on AWS. It includes steps for configuring AWS services like ECR, ECS, and Load Balancer.

## Project Steps

1. **Create an EC2 Instance**: 
   - Launch an EC2 instance and install Docker.
2. **Setup Docker**:
   - Create a `Dockerfile` to build the Apache HTTP server using an Ubuntu base image.
   - Build and run the Docker container exposing Apache on port 80.
3. **Push Image to ECR**:
   - Create a private ECR repository and push your Docker image to it.
4. **Set Up IAM Roles**:
   - Create IAM roles for EC2 and ECS with appropriate permissions.
5. **Install AWS CLI**:
   - Configure the AWS CLI with your access keys.
6. **Create Load Balancer**:
   - Set up an Application Load Balancer to distribute traffic.
7. **Create ECS Cluster**:
   - Define tasks and services to run your Docker container using the image from ECR.

## Dockerfile

Below is the `Dockerfile` used in this project:

```Dockerfile
# Use the official Ubuntu base image
FROM ubuntu:latest

# Update package list and install Apache HTTP server
RUN apt-get update && apt-get install -y apache2

# Copy index.html to the default Apache document root
COPY index.html /var/www/html/

# Command to run when the container starts, to keep Apache HTTP server running in the foreground
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

# Expose port 80 to allow incoming HTTP traffic
EXPOSE 80



# Build the Docker image
docker build -t project-image .

# Run the Docker container
docker run -itd -p 80:80 --name project project-image
