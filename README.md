# Retail Banking App Deployment Using Terraform

Date: 17/10/2023

Done by: Nehemiah Monrose

## Table of Contents
- [Purpose](#purpose)
- [Requirements](#requirements)
- [Steps](#steps)
- [Optimization](#optimization)
- [Diagram](#diagram)




## Purpose

The purpose of this documentation is to demonstrate the process it took to deploy a Retail Banking App with Terraform which is an Infrastructure-As-Code provisioning tool used for building, changing, and versioning our infrastructure safely and efficiently, and Jenkins which is used to create, manage, and automate our CI/CD (Continous Integration/Continuous Deployment) pipeline.

## Requirements
Use Terraform to create:
- 1 VPC
- 2 Availability Zones
- 2 Public Subnets
- 2 EC2S
- 1 Route Table
- Security Group Ports: 8080, 8000, 22
- Jenkins CI/CD pipeline


## Steps

1. **Create a New GitHub Repository**
   - Go to https://github.com and log in to your GitHub account.
   - Click on the "+" icon in the top-right corner and select "New repository."
   - Follow the prompts to create a new repository with an appropriate name and description.
   
2. **Clone the New Repository**
   - Open your terminal/command prompt.
   - Navigate to the directory where you want to store the repository.
   - Clone your new repository using the following command, replacing `[repository_url]` with your repository's URL:
     ```
     git clone [repository_url]
     ```

3. **Download Files from Existing Repository**
   - Navigate to the existing repository that contains the application files.
   - Click on the "Code" button and copy the repository's URL.
   - Open your terminal/command prompt.
   - Navigate to the directory where you want to store the files.
   - Use the following command to download the files into your new repository, replacing `[existing_repository_url]` with the existing repository's URL:
     ```
     git clone [existing_repository_url]
     ```


4. **Jenkins Setup on First Ec2 Instance**
   - Installed Jenkins on my first EC2 Instance called tf_jenkins_server
   - Created a new user account and password for Jenkins
   - Generated SSH Key to be able to SSh into the second EC2 Instance retail_banking server
  
8. **Create and Configure the Jenkins pipeline
   - Click New Item in the left panel
   - Give a name to the pipeline
   - Select Multibranch pipeline
   - Connect Github to pipeline(Username, PAT(Personal Access Token), Repository HTTP URL)
   - The JenkinsfileV1 runs the app setup.sh on the server

10. **Edit Jenkins file**
    -Add clean, and deploy stages   


## Optimization

To optimize the deployment, consider the following:

- **Scaling**: If the application's load varies, consider implementing auto-scaling mechanisms to handle increased traffic automatically.

- **Content Delivery Networks (CDNs)**: Utilize CDNs to cache and serve static assets, reducing server load and latency.

- **Load Balancing**: Implement load balancing to distribute traffic evenly across multiple servers or instances.

- **Containerization**: Consider containerizing the application using technologies like Docker for easier deployment and scaling.


## Diagram
