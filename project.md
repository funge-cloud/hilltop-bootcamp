

# **Task 1: Modify and Deploy the Dockerized Application with Terraform**  
#### **Objective**  
Engineers will modify the application, update the Dockerfile, and deploy the Dockerized application on an EC2 instance provisioned using Terraform.  

#### **Description**  
1. Clone the repository: [hilltop-docker](https://github.com/HILL-TOPCONSULTANCY/hilltop-docker.git).  
2. Modify the `app.js` file to include a log statement:  
   ```javascript  
   console.log("App built by [Your Name].");  
   ```  
3. Update the `Dockerfile` to include two environment variables:  
   - `STUDENT_NAME` (your name)  
   - `STUDENT_EMAIL` (your email address)  
4. Write Terraform files to:  
   - Create an AWS EC2 instance (`t3.midium`) in a public subnet.  
   - Add a security group to allow HTTP traffic on port 80.  
5. Use a `user_data` script in Terraform to:  
   - Install Docker on the instance.  
   - Build the Docker image locally on the server.  
   - Tag the image with your Docker Hub username.  
   - Push the image to your Docker Hub repository.  
   - Run the container, exposing port 8080 and forwarding it to port 80 on the server.  

#### **Requirements**  
- Modified `app.js` and updated `Dockerfile`.  
- Terraform files provisioning the EC2 instance and configuring the application.  
- Docker image built and pushed to Docker Hub.  
- Application accessible via the EC2 public IP.  

#### **Deliverables**  
1. Modified `app.js` file and updated `Dockerfile`.  
2. Terraform files (`main.tf`, `variables.tf`, `outputs.tf`).  
3. Screenshot of the app running on the EC2 instance's public IP.  
4. URL to the Docker Hub repository with the pushed image.  

#### **Instructions**  
1. Modify the repository files as required.  
2. Write Terraform configurations to provision the infrastructure.  
3. Deploy the infrastructure:  
   ```bash  
   terraform init  
   terraform apply  
   ```  
4. Verify the application by accessing `http://<EC2_PUBLIC_IP>`.  

---

# **Task 2: Automate the Build and Deployment with Jenkins**  
#### **Objective**  
Students will use Terraform to provision a Jenkins server and set up a CI/CD pipeline for automating the build, test, and deployment process.  

#### **Description**  
1. Write Terraform files to:  
   - Create a new EC2 instance (`t3.meduim`) in a public subnet for Jenkins.  
   - Add a security group to allow HTTP and SSH access.  
   - Use a `user_data` script to install Jenkins and start the Jenkins service.  
2. Configure Jenkins to:  
   - Clone the `hilltop-docker` repository.  
   - Build the Docker image.  
   - Tag the image with a new version (e.g., `dockerhubusername/bao-app:v2.0`).  
   - Push the image to Docker Hub.  
   - Deploy the updated application to the first EC2 instance from Task 1 using SSH to stop the existing container and run the updated image.  

#### **Requirements**  
- Terraform files for provisioning the Jenkins server.  
- A fully functional Jenkins pipeline.  

#### **Deliverables**  
1. Terraform files for the Jenkins server (`main.tf`, `variables.tf`, `outputs.tf`).  
2. Screenshot of the Jenkins dashboard showing a successful pipeline run.  
3. Screenshot of the updated app running on the first EC2 instance.  

#### **Instructions**  
1. Write the Terraform configurations to deploy the Jenkins server.  
2. Configure the Jenkins pipeline using the following stages:  
   - **Clone Repository**  
   - **Build Docker Image**  
   - **Push Docker Image**  
   - **Deploy Application**  
3. Test the pipeline by pushing a new update to the `app.js` file in the repository.  
4. Verify the application on the EC2 instance by checking for the updated log message.  

---

### **Task Summary**  

### **Task 1**  
- Modify the app and Dockerfile.  
- Deploy it to an EC2 instance using Terraform and Docker.  

#### **Task 2**  
- Automate the build and deployment process using Jenkins, with a Jenkins pipeline running on a separate EC2 instance.  

