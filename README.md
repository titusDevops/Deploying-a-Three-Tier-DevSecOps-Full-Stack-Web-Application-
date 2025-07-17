
# Deploying a Three-Tier DevSecOps Full Stack Web Application on AWS EKS using ArgoCD, Prometheus, Grafana and Jenkins 
Deploy a secure and scalable three-tier web application on AWS EKS using Docker and DevSecOps best practices. This project automates CI/CD with Jenkins, ArgoCD, SonarQube, and Trivy for code quality and security, while Prometheus and Grafana provide real-time monitoring. It leverages AWS services like ECR, S3, EC2, and DynamoDB, with Terraform managing full Infrastructure as Code (IaC) for seamless provisioning and deployment.



![Screenshot 2025-07-02 211523](https://github.com/user-attachments/assets/f1438274-7c29-4297-ace1-2ba07291e350)


# 1) IAM User Setup:
### Creating an IAM user with the necessary permissions for EKS, S3, DynamoDB, ECR, and EC2.

  * #### On AWS Console, search I am, and click Users.
  

<img width="1914" height="909" alt="Screenshot 2025-07-13 100602" src="https://github.com/user-attachments/assets/f95c241e-49cc-4762-ab7a-37109bd2d86c" />


* #### Giving a username to my I am User.


<img width="1892" height="920" alt="Screenshot 2025-07-13 100833" src="https://github.com/user-attachments/assets/4eee0c37-3496-4b90-9cde-e59f1f4d9c0d" />


* #### Attaching the administrative access for testing and then click Create user.


<img width="1904" height="910" alt="Screenshot 2025-07-13 100931" src="https://github.com/user-attachments/assets/a316f02d-1b42-471e-88e6-6e5f43f4c360" />



* #### Creating an access and secret access keys.


<img width="1905" height="910" alt="Screenshot 2025-07-13 101204" src="https://github.com/user-attachments/assets/b0741591-9ada-4de3-bbc9-cdd810e99291" />


<img width="1902" height="911" alt="Screenshot 2025-07-13 101323" src="https://github.com/user-attachments/assets/eb5ba139-558e-4788-82d5-84679ce23b1f" />


* #### Download the file for later use of the secret key and access key.


<img width="1904" height="910" alt="Screenshot 2025-07-13 101342" src="https://github.com/user-attachments/assets/f20db528-a238-4c1e-a9dc-46f6997feab9" />


# 2) Terraform & AWS CLI Installation:

### Installing Terraform and AWS CLI on my local machine and configuring AWS CLI with IAM credentials.

* #### To install Terraform, I visited [Terraform official website](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli).

* #### To install AWS CLI, I visited [AWS installation page](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

 <img width="1285" height="529" alt="Screenshot 2025-07-15 092748" src="https://github.com/user-attachments/assets/13f13189-bc39-4974-a4a2-9fcaf414d5b4" />

* #### After installation, I verified installation with these two commands below:
  
 <img width="1919" height="553" alt="Screenshot 2025-07-15 092803" src="https://github.com/user-attachments/assets/4695eea4-98df-4ba8-8af9-b6fea69ba944" />

* #### Then I configured AWS CLI using the given below commands. I used Access and Secret Keys from the CSV file that I downloaded in the IAM User Setup.
 
 <img width="1890" height="413" alt="Screenshot 2025-07-15 094400-redacted_dot_app (1)" src="https://github.com/user-attachments/assets/0272a747-83c1-45c2-986f-576265a19d38" />


# 3) S3 Bucket and DynamoDB Table:

### I am creating S3 Bucket and Dynamo DB as they are required for Terraform's backend state.

* #### Created an S3 bucket successfully and the S3 bucket name has to be a unique name.


 <img width="1906" height="759" alt="Screenshot 2025-07-15 103649" src="https://github.com/user-attachments/assets/7e385150-8e0c-430c-a284-8aa43afb3a33" />


* #### Created a DynamoDB table successfully and the DynamoDB table name will be lock-files  , and the partition key will be LockID.
  
<img width="1919" height="898" alt="Screenshot 2025-07-15 104845" src="https://github.com/user-attachments/assets/0e16463f-8157-4ad0-82d2-061242df7531" />

# 4) Jenkins EC2 Server Setup with Terraform:

* #### Next, we have to run the command to create .pem file for our Jenkins instance. will be used to ssh the server

<img width="1671" height="131" alt="Screenshot 2025-07-15 114913" src="https://github.com/user-attachments/assets/1297b37f-94db-4c0a-8c98-cf1e37493788" />

<img width="1442" height="548" alt="Screenshot 2025-07-15 152055" src="https://github.com/user-attachments/assets/393001eb-e790-4fdf-82a8-480ed71ba399" />

<img width="1454" height="84" alt="Screenshot 2025-07-15 152140" src="https://github.com/user-attachments/assets/f9eb6736-cd25-4781-8a26-05ba952640fa" />

<img width="1579" height="641" alt="Screenshot 2025-07-16 081150" src="https://github.com/user-attachments/assets/138df48f-61a5-4a01-a102-1604ac7888be" />

<img width="1579" height="641" alt="Screenshot 2025-07-16 081150" src="https://github.com/user-attachments/assets/12f14fbb-ffdc-4367-ae82-f2928c9e6607" />

<img width="1426" height="763" alt="Screenshot 2025-07-16 081245" src="https://github.com/user-attachments/assets/4ddbe5a3-1878-436c-969d-551e3830d4f7" />

<img width="1437" height="761" alt="Screenshot 2025-07-16 081317" src="https://github.com/user-attachments/assets/523f3138-50bb-4b6c-a13e-851099e016d2" />


<img width="1420" height="733" alt="Screenshot 2025-07-16 082750" src="https://github.com/user-attachments/assets/81dee992-6dbe-4cd9-82cd-aab78c2d0e20" />

<img width="1885" height="949" alt="Screenshot 2025-07-16 102240" src="https://github.com/user-attachments/assets/cf657ee8-d3f1-448d-83dc-961ea15add4e" />
<img width="1891" height="969" alt="Screenshot 2025-07-16 102308" src="https://github.com/user-attachments/assets/c61a8cb6-92af-4d84-88df-4472e1f52dcd" />
<img width="1893" height="985" alt="Screenshot 2025-07-16 102326" src="https://github.com/user-attachments/assets/bb84018f-740a-40ee-a3f3-095ef3144236" />

# 5) Installing Plugins on Jenkins
Open the EC2-IP:8080 in the browser. 
<img width="1903" height="1015" alt="Screenshot 2025-07-16 110851" src="https://github.com/user-attachments/assets/e294b07e-f642-44a7-8ea5-da9eab6d65eb" />
<img width="1907" height="936" alt="Screenshot 2025-07-16 111032" src="https://github.com/user-attachments/assets/91a0966e-68fe-429c-882b-195951f1455c" />

You can get the password of Jenkins
<img width="1458" height="156" alt="Screenshot 2025-07-16 111048" src="https://github.com/user-attachments/assets/713d50cd-a7c5-4fbd-a4c6-af94d6709b99" />

We have to install all these mentioned plugins.
AWS Credentials
AWS Steps
Docker plugins
Eclipse Temurin installer
NodeJS
OWASP Dependency-Check,
SonarQube Scanner.


# 6) SonarQube Setup
Open Sonarrqube in the browser. 

http://<jenkins-server-public-ip>:9090

username and password for sonarqube is admin.



Next, We have to perform 5 Steps on the sonarqube setup.

Setup of frontend project for code analysis
Setup of backend project for code analysis
Replace the keys in jenkins-pipeline folder, you got from the above two steps. (watch video sonarqube setup)
create a sonar-token, and save it somewhere for later use in Jenkins.
create a webhook on the sonarqube dashboard. (http://<jenkins-ec2-server-public-ip>:8080/sonarqube-webhook/)

# 7) Amazon ECR Repositories
Create two repositories, one for the backend and front end.

Login to ECR on the Jenkins server, using the ECR push command.


# 7a) Add Cred. in Jenkins
Got to Manage Jenkins -> Credentials.

We have to add here a total of 7 Credentials.
Now We have to configure the installed plugins. (important)

In Tools, We have to configure JDK, sonar-scanner, nodejs, DP-Check, and docker.

Go to Dashboard -> Manage Jenkins -> System

Search for SonarQube installations

Provide the name as it is, then in the Server URL copy the sonarqube public IP (same as Jenkins) with port 9000 select the sonar token that we have added recently, and click on Apply & Save.
# 8) EKS Cluster Deployment
We have to create EKS Cluster using the below commands.

Once the cluster is ready, you can validate if the nodes are ready or not.

Now, we will configure the Load Balancer on our EKS because our application will have an ingress controller.
Download the policy for the LoadBalancer prerequisite.

Create the IAM policy using the below command

Create OIDC Provider

Create a Service Account by using below command and replace your account ID with your one
Run the below command to deploy the AWS Load Balancer Controller

After 2-3 minutes, run the command below to check whether your pods are running or not.
# 9) Prometheus and Grafana Installation and Configuration
What is Grafana?

Grafana is an open-source platform for visualization and analytics. It allows you to query, visualize, alert on, and explore metrics from various data sources.

Steps to Install and Configure Prometheus and Grafana on Kubernetes

Step 1: Add Helm Repositories

Add Helm Stable Chart Repository
2. Add Prometheus Community Helm Repository

Step 2: Create a Namespace for monitoring

Step 3: Install Prometheus with Grafana using Helm

Install the kube-prometheus-stack chart, which includes both Prometheus and Grafana:
This command deploys Prometheus and Grafana as part of the kube-prometheus-stack in the prometheus namespace on your EC2 instance.

Step 4: Verify Prometheus Installation

Check the Prometheus pods:
This command deploys Prometheus and Grafana as part of the kube-prometheus-stack in the prometheus namespace on your EC2 instance.

Step 4: Verify Prometheus Installation

Check the Prometheus pods:
Check the Prometheus services:

Since Grafana is deployed along with Prometheus, there is no need for separate Grafana installation.

Step 5: Expose Prometheus and Grafana to External Access

There are two ways to expose these services:

NodePort
LoadBalancer

Exposing Prometheus via LoadBalancer:
Save the file. The service should now have a load balancer with an external IP to access Prometheus.

Exposing Grafana via LoadBalancer:

Similarly, edit the Grafana service configuration to change ClusterIP to LoadBalancer:
Save the changes and use the load balancer IP in your browser to access Grafana.

Step 6: Accessing Grafana

The username will be admin and the password will be prom-operator for your Grafana LogIn.
# 10) Jenkins Pipelines (Frontend & Backend)
# 11) ArgoCD Installation & Application Deployment
Now, we will install argoCD.

To do that, create a separate namespace for it and apply the argocd configuration for installation
All pods must be running, to validate run the below command
Now, expose the argoCD server as LoadBalancer using the below command

You can validate whether the Load Balancer is created o by going to the AWS Console load balancers.

To access the argoCD, copy the LoadBalancer DNS CNAME record and hit on your favorite browser.

Now, we need to get the password for our argoCD server to perform the deployment.

To do that, we have a pre-requisite which is jq. Install it by the command below.
Next will deploy our Three-Tier Application using ArgoCD

As our repository is private. So, we need to configure the Private Repository in ArgoCD.

Then We have to set up applications.


