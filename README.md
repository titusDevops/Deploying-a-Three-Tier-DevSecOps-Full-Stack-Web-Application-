
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










