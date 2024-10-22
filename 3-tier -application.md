#                                                                              **Project Description**

The project aims to develop a simple full-stack web application that leverages **AWS infrastructure** using **Terraform** for the underlying infrastructure setup, 
including a **VPC**, an **EKS cluster** with two nodes, and the necessary networking components. The application has a **frontend (FE)**, **backend (BE)**, and **MongoDB database** (DB), 
which are deployed on the **Amazon EKS cluster**. The frontend serves a dashboard where users can input information that is then processed and stored in the MongoDB database via the backend. 
The information submitted by the users is visible in real-time on the dashboard in a tabular format.

The deployment will be automated using **Helm** to manage Kubernetes resources, ensuring the application scales efficiently and can be managed via EKS. 
Each component of the application (FE, BE, and DB) will run in specific subnets and on designated ports to maintain separation and ensure security.

---

### **Architecture**:

#### **1. VPC (Virtual Private Cloud)**:
- The application will be deployed within a custom **VPC** in a specific region (e.g., **eu-central-1**). The VPC will be divided into **public and private subnets**.
   - **Public Subnets**: The frontend application will be deployed in public subnets to allow users to access the UI from the internet.
   - **Private Subnets**: The backend (API) and MongoDB database will be deployed in private subnets, isolated from direct internet access for security.
   
   The VPC architecture will include the following:
   - **Internet Gateway**: To allow internet traffic to reach the frontend.
   - **NAT Gateway**: For backend instances to initiate outbound connections to the internet (for things like API calls or updates) while being unreachable from the internet.
   - **Route Tables**: Define how traffic flows between the subnets, ensuring that traffic to the frontend can be routed to the backend and database.

#### **2. Amazon EKS (Elastic Kubernetes Service)**:
- An **EKS cluster** will be deployed within the VPC. This cluster will consist of **two worker nodes** distributed across private subnets for high availability. 
   - **Node Groups**: Each node group will be provisioned using **Terraform** to ensure consistency across environments.
   - **Helm** will be used to manage Kubernetes resources within the EKS cluster, ensuring that deployments are standardized, repeatable, and scalable.

#### **3. Application Components**:
The application consists of three main tiers:
   
   **a. Frontend (FE)**:
   - The **frontend** is a simple web-based dashboard (built with React, Angular, or any web framework of choice). It will be deployed in the **public subnet** and exposed via an **Elastic Load Balancer (ELB)**.
   - Users will interact with the frontend to submit data, which is then sent to the backend via HTTP requests. The frontend will also fetch data from the backend and display it in a tabular format on the UI.
   - **Port**: The frontend will listen on port **80** for HTTP traffic.

   **b. Backend (BE)**:
   - The **backend** is a service (built with Node.js, Python, or similar) that handles requests from the frontend and interacts with the **MongoDB** database.
   - It provides RESTful API endpoints to submit and fetch data, such as `/submit` and `/fetch`. When a user submits data through the frontend,
   - the backend processes it and stores it in MongoDB. The backend will also fetch data from the database to display it on the dashboard.
   - The backend service will be deployed in a **private subnet** and will not be exposed directly to the internet.
   - **Port**: The backend service will listen on port **8080**.

   **c. MongoDB Database (DB)**:
   - MongoDB will be deployed in a **private subnet** to ensure that it is not publicly accessible. Only the backend service will be able to interact with it.
   - The database will store the information submitted by users and make it available for querying when requested by the backend.
   - **Port**: MongoDB will run on port **27017**, and access will be restricted to the backend service.

#### **4. Networking and Security**:
- **Security Groups**: Security groups will be configured to allow traffic between the different tiers of the application. For example, the frontend can communicate with the backend over port 8080, and the backend can communicate with MongoDB over port 27017.
- **Subnets and Routing**: Each tier will be deployed in specific subnets to ensure isolation between public-facing and private resources. Traffic between tiers will be routed through internal VPC networking, ensuring that sensitive services like MongoDB are not exposed externally.

---

### **Application Flow**:

1. **User Interaction**:
   - A user accesses the **frontend UI** through their browser and submits data via a form on the dashboard. This form contains fields like `name`, `email`, and `message`.

2. **Data Submission**:
   - When the user clicks "Submit," the frontend sends the data via an HTTP POST request to the backend API (e.g., `/submit`).

3. **Backend Processing**:
   - The backend receives the data, processes it, and inserts it into the **MongoDB database** via a secure connection.
   - A response is sent back to the frontend to confirm that the data has been successfully stored.

4. **Database Interaction**:
   - The MongoDB database stores the submitted data in a structured format. This data is accessible to the backend whenever needed.

5. **Fetching Data**:
   - The frontend periodically sends GET requests to the backend to fetch all submitted data (e.g., via an API endpoint like `/fetch`). 
   - The backend retrieves the data from MongoDB and sends it back to the frontend, where it is displayed in a tabular format on the dashboard for the user to see.

6. **Dashboard Update**:
   - As the user submits data, the dashboard is updated in real-time (or on refresh) to display the newly added information in the table.

---

### **Deployment Process Using Helm**:

1. **Helm Charts**:
   - **Helm** will be used to package the Kubernetes resources (Deployment, Service, ConfigMap, etc.) for each component (frontend, backend, and MongoDB).
   - Each component will have its own Helm chart that defines its deployment strategy, resource allocation (e.g., CPU and memory), and service configuration (e.g., ClusterIP for backend and LoadBalancer for frontend).

2. **Helm Deployment**:
   - Deploy the **MongoDB Helm chart** into the EKS cluster's private subnet.
   - Deploy the **backend Helm chart** into the private subnet and expose it internally to the frontend.
   - Deploy the **frontend Helm chart** into the public subnet and expose it via an Elastic Load Balancer for external access.

3. **EKS Cluster Management**:
   - The **EKS cluster** will manage the lifecycle of the application, ensuring high availability and scaling of pods as needed.
   - Each component (FE, BE, and DB) will run in its own **Kubernetes pod**, and the application will benefit from EKS's autoscaling and self-healing features.

---

This design outlines the infrastructure, architecture, and application flow for deploying a full-stack application using **AWS**, **Terraform**, **EKS**, and **Helm**. 
By structuring the deployment into distinct tiers (frontend, backend, database) and using Terraform for infrastructure provisioning and Helm for application deployment, the solution provides scalability, security, and ease of management.
