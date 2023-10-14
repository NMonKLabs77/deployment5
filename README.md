# Retail Banking App Deployment Using Terraform

Date: 3/10/203

Done by: Nehemiah Monrose

## Table of Contents
- [Purpose](#purpose)
- [Steps](#steps)
- [Optimization](#optimization)
- [Diagram](#diagram)




## Purpose

The purpose of this documentation is to guide you through the process I took to deploy my application to the NGINX Web server and monitor the performance of my application using Cloud Watch. Cloud Watch is an AWS service that allows me to monitor the performance of my application using various metrics.


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

4. **Step #3 Setup VPC and EC2 Infrastructure** 

   - Setup and Configure a new VPC

   - Create a public subnet

   - Connect to public Route Table

   - Connect to Internet Gateway
  
5. **Initialize EC2 Instance**
   - Navigate to https://us-east-1.console.aws.amazon.com
   - In the search bar at the top, type EC2
   - Click EC2 service
   - Click Instances
   - Click Launch Instances
   - Name your Instance
   - Select UBUNTU
   - Click Instance Type and Select t2.medium
   - Select Key pair
   - Edit network settings
   - Choose VPC
   - For subnet choose VPC created
   - Enable Auto-Assign IP
   - Create a security group with ports 22, 80,8080 and 8000
   - Click Launch Instance


6. **Install and Configure Dependencies**
   - Install "python3.10-venv", "python3-pip" and "zip"
   - Install NGINX
   - Edit the configuration file "/etc/nginx/sites-enabled/default"
  <img width="606" alt="Screenshot 2023-10-03 at 11 35 39 AM" src="https://github.com/NMonKLabs77/deployment4/assets/139259756/d5d9830f-b85d-4818-9e07-f2cb4e6cc788">

     

7. **Install Jenkins**
   - Update the server: ```sudo apt-get update```
   - Add the key to our system: ``` curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null```

   - Add Jenkins apt repository entry: ```   
  echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null```

  - Update server again: ```  sudo apt-get update```
  - Install java: ```  sudo apt-get install fontconfig openjdk-17-jre```
  - Install Jenkins:  ```sudo apt-get install jenkins```
  - Start Jenkins server: ```sudo systemctl start jenkins```
  - ```sudo cat /var/lib/jenkins/secrets/initialAdminPassword``` to get the Admin Password
  - Install suggested plugins
  - Install plugin Pipeline Utility Steps

8. **Create and Configure the Jenkins pipeline
   - Click New Item in the left panel
   - Give a name to the pipeline
   - Select Multibranch pipeline
   - Connect Github to pipeline(Username, PAT(Personal Access Token), Repository HTTP URL)

9. **Configure Github Webhook**
    - From the repository main page navigate to settings
    - Click Webhooks
    - Click Add webhook
    - Click Payload Url Field and enter: "http://your_Jenkins_IP_Address:8080/github-webhook/"
    - Click Add Webhook

  <p>When any changes are made in a file, for example, the Jenkin File in the GitHub repository, the changes will automatically be pushed to Jenkin, and Jenkins will then run and test the stages again</p>
  
10. **Edit Jenkins file**
    -Add clean, and deploy stages   

 <img width="762" alt="Screenshot 2023-10-03 at 3 54 16 PM" src="https://github.com/NMonKLabs77/deployment4/assets/139259756/6b5daffd-3bcc-4cc4-92ee-52fc24b09755">


11. **Monitoring**
    - Navigate to Cloud Watch
    - In the left panel click All Alarms
    - Click Create Alarm
    - Select Metric
    - Select t2.medium: Cpu_usage_user
    - Set name, alert message, topic threshold etc
    - Stress test </br>



    <img width="1181" alt="Screenshot 2023-10-03 at 10 47 26 PM" src="https://github.com/NMonKLabs77/deployment4/assets/139259756/5f4afeec-3d21-4975-b014-77259e0c71d8">

    Here is a snapshot of the email sent:
    

<img width="1085" alt="Screenshot 2023-10-03 at 10 45 16 PM" src="https://github.com/NMonKLabs77/deployment4/assets/139259756/ca6edbfc-b06a-4a55-9b19-5ca6b2bb8d70">



12. **Results of Deployment**
    <p>URL Shortener was successfully deployed to Nginx Server!!</p>

    <img width="1440" alt="Screenshot 2023-10-03 at 10 59 17 PM" src="https://github.com/NMonKLabs77/deployment4/assets/139259756/76c8bd06-7ab4-466a-9ee7-cb9d5c3b5fba">



## Optimization

To optimize the deployment, consider the following:

- **Scaling**: If the application's load varies, consider implementing auto-scaling mechanisms to handle increased traffic automatically.

- **Content Delivery Networks (CDNs)**: Utilize CDNs to cache and serve static assets, reducing server load and latency.

- **Load Balancing**: Implement load balancing to distribute traffic evenly across multiple servers or instances.

- **Containerization**: Consider containerizing the application using technologies like Docker for easier deployment and scaling.


## Diagram
