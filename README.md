# Three-Tier DevSecOps Web Application   

Deployed a **secure and scalable** three-tier web application on AWS EKS, leveraging Docker and DevSecOps practices. Automated CI/CD pipelines with Jenkins, Trivy, and SonarQube for secure, high-quality code delivery. Implemented GitOps using ArgoCD for seamless deployments via Git repositories. Set up Prometheus and Grafana for real-time monitoring with intuitive dashboards. Utilized Terraform for Infrastructure as Code, managing AWS services like ECR, S3, EC2, and DynamoDB for production-ready deployment.

<img width="788" height="473" alt="Screenshot 2025-07-17 223454" src="https://github.com/user-attachments/assets/12103aea-e84a-4bda-b036-212fbd00e639" />


***


# 1) IAM User Setup:
### Created an IAM user with the necessary permissions for EKS, S3, DynamoDB, ECR, and EC2.

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


***

# 2) Terraform & AWS CLI Installation:

### Installing Terraform and AWS CLI on my local machine and configuring AWS CLI with IAM credentials.

* #### To install Terraform, I visited [Terraform official website](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli).

* #### To install AWS CLI, I visited [AWS installation page](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

 <img width="1285" height="529" alt="Screenshot 2025-07-15 092748" src="https://github.com/user-attachments/assets/13f13189-bc39-4974-a4a2-9fcaf414d5b4" />

* #### After installation, I verified installation with these two commands below:
  
 <img width="1919" height="553" alt="Screenshot 2025-07-15 092803" src="https://github.com/user-attachments/assets/4695eea4-98df-4ba8-8af9-b6fea69ba944" />

* #### Then I configured AWS CLI using the given below commands. I used Access and Secret Keys from the CSV file that I downloaded in the IAM User Setup.
 
 <img width="1890" height="413" alt="Screenshot 2025-07-15 094400-redacted_dot_app (1)" src="https://github.com/user-attachments/assets/0272a747-83c1-45c2-986f-576265a19d38" />


***


# 3) S3 Bucket and DynamoDB Table:

### I am creating S3 Bucket and Dynamo DB as they are required for Terraform's backend state.

* #### Created an S3 bucket successfully and the S3 bucket name has to be a unique name.


 <img width="1906" height="759" alt="Screenshot 2025-07-15 103649" src="https://github.com/user-attachments/assets/7e385150-8e0c-430c-a284-8aa43afb3a33" />


* #### Created a DynamoDB table successfully and the DynamoDB table name will be lock-files  , and the partition key will be LockID.
  
<img width="1919" height="898" alt="Screenshot 2025-07-15 104845" src="https://github.com/user-attachments/assets/0e16463f-8157-4ad0-82d2-061242df7531" />


***

# 4) Jenkins EC2 Server Setup with Terraform:


* #### configure aws on the Jenkins server(EC2 Instance). As you did for your local machine.

* #### Next, I ran a command to create .pem file for my Jenkins instance. It will be used to ssh into the server.
* #### Now run this command to create a Jenkins server.


<img width="1671" height="131" alt="Screenshot 2025-07-15 114913" src="https://github.com/user-attachments/assets/1297b37f-94db-4c0a-8c98-cf1e37493788" />

* #### terraform init


<img width="1442" height="548" alt="Screenshot 2025-07-15 152055" src="https://github.com/user-attachments/assets/393001eb-e790-4fdf-82a8-480ed71ba399" />

* #### terraform validate


<img width="1454" height="84" alt="Screenshot 2025-07-15 152140" src="https://github.com/user-attachments/assets/f9eb6736-cd25-4781-8a26-05ba952640fa" />


* #### terraform plan


<img width="1579" height="641" alt="Screenshot 2025-07-16 081150" src="https://github.com/user-attachments/assets/138df48f-61a5-4a01-a102-1604ac7888be" />




<img width="1579" height="641" alt="Screenshot 2025-07-16 081150" src="https://github.com/user-attachments/assets/12f14fbb-ffdc-4367-ae82-f2928c9e6607" />


* #### terraform apply
  
<img width="1426" height="763" alt="Screenshot 2025-07-16 081245" src="https://github.com/user-attachments/assets/4ddbe5a3-1878-436c-969d-551e3830d4f7" />

<img width="1437" height="761" alt="Screenshot 2025-07-16 081317" src="https://github.com/user-attachments/assets/523f3138-50bb-4b6c-a13e-851099e016d2" />

<img width="1420" height="733" alt="Screenshot 2025-07-16 082750" src="https://github.com/user-attachments/assets/81dee992-6dbe-4cd9-82cd-aab78c2d0e20" />

* #### chmod 400 "devsecops-project.pem"
* #### ssh -i "devsecops-project.pem" ubuntu@35.92.246.29


<img width="1885" height="949" alt="Screenshot 2025-07-16 102240" src="https://github.com/user-attachments/assets/cf657ee8-d3f1-448d-83dc-961ea15add4e" />

<img width="1891" height="969" alt="Screenshot 2025-07-16 102308" src="https://github.com/user-attachments/assets/c61a8cb6-92af-4d84-88df-4472e1f52dcd" />

<img width="1893" height="985" alt="Screenshot 2025-07-16 102326" src="https://github.com/user-attachments/assets/bb84018f-740a-40ee-a3f3-095ef3144236" />


***


# 5) Installing Plugins on Jenkins
* #### Opening the EC2-IP:8080 in the browser.
 
<img width="1903" height="1015" alt="Screenshot 2025-07-16 110851" src="https://github.com/user-attachments/assets/e294b07e-f642-44a7-8ea5-da9eab6d65eb" />

<img width="1907" height="936" alt="Screenshot 2025-07-16 111032" src="https://github.com/user-attachments/assets/91a0966e-68fe-429c-882b-195951f1455c" />

* #### Retreiving the password of Jenkins and logging in

<img width="1458" height="156" alt="Screenshot 2025-07-16 111048" src="https://github.com/user-attachments/assets/713d50cd-a7c5-4fbd-a4c6-af94d6709b99" />

<img width="1903" height="903" alt="Screenshot 2025-07-16 111954" src="https://github.com/user-attachments/assets/20582975-7fc2-447f-8c9f-7d374181157e" />

<img width="1444" height="900" alt="Screenshot 2025-07-16 112056" src="https://github.com/user-attachments/assets/0ea11b5f-42b5-4e7e-9aea-71926650a795" />

<img width="1889" height="905" alt="Screenshot 2025-07-16 112117" src="https://github.com/user-attachments/assets/cc7b3911-f4ec-4f6d-be67-43d3db9aa255" />

* #### Welcome to Jenkins

<img width="1896" height="890" alt="Screenshot 2025-07-16 114502" src="https://github.com/user-attachments/assets/6734cc6a-29f8-4678-8306-81bbdf65e2a1" />

* #### Installing all 7 plugins that is  AWS Credentials, AWS Steps, Docker plugins, Eclipse Temurin installer, NodeJS, OWASP Dependency-Check and SonarQube Scanner
  
<img width="1897" height="886" alt="Screenshot 2025-07-16 121947" src="https://github.com/user-attachments/assets/9de81502-f14d-43f8-a121-96bc15670c76" />

<img width="1897" height="886" alt="Screenshot 2025-07-16 121947" src="https://github.com/user-attachments/assets/048c5514-392d-4bd2-97a8-e06645eccbb7" />

* #### Plugin installation sucess

<img width="1902" height="881" alt="Screenshot 2025-07-16 122514" src="https://github.com/user-attachments/assets/42b0d0fa-4b78-40b9-9605-b249eaeb38b1" />


***


# 6) SonarQube Setup
* #### I opened Sonarrqube in the browser at http://<jenkins-server-public-ip>:9090 and the username and password for sonarqube is admin. But update the password after logging in.

<img width="1904" height="1005" alt="Screenshot 2025-07-16 123200" src="https://github.com/user-attachments/assets/5136bcf4-c7e2-4bef-a843-f05f3fa4e7f1" />

<img width="1080" height="689" alt="Screenshot 2025-07-16 123315" src="https://github.com/user-attachments/assets/633bdecb-d71c-4e4c-bee4-7c114631c732" />


* #### I performed 5 Steps on the sonarqube setup.

* #### Setup of frontend project for code analysis
  
<img width="1916" height="764" alt="Screenshot 2025-07-16 123909" src="https://github.com/user-attachments/assets/3e71e004-23cd-48ae-b47b-49c3f7bf769a" />

<img width="1782" height="778" alt="Screenshot 2025-07-16 124048" src="https://github.com/user-attachments/assets/bf8c4ee3-05ba-4515-9b5a-13cf3b802e7c" />

* #### Setup of backend project for code analysis
  
<img width="1916" height="858" alt="Screenshot 2025-07-16 123938" src="https://github.com/user-attachments/assets/f327179f-90a8-41b4-a81f-8df8a08885e0" />

<img width="1893" height="886" alt="Screenshot 2025-07-16 125004" src="https://github.com/user-attachments/assets/0610c814-014e-4a42-bca3-f6ef5c74bcaa" />

* #### I created a sonar-token, and saved it somewhere for later use in Jenkins

<img width="1758" height="735" alt="Screenshot 2025-07-16 125608" src="https://github.com/user-attachments/assets/1d92de96-288a-4d42-b904-46814146627f" />

* #### I created a webhook on the sonarqube dashboard. (http://<jenkins-ec2-server-public-ip>:8080/sonarqube-webhook/)

<img width="1881" height="876" alt="Screenshot 2025-07-16 125945" src="https://github.com/user-attachments/assets/351b3483-1517-426e-bb0c-c76bd440cda4" />

<img width="1904" height="863" alt="Screenshot 2025-07-16 130050" src="https://github.com/user-attachments/assets/8c4c0f36-142f-4e95-8186-064e2320cea7" />


***

# 7) Amazon ECR Repositories

* #### Created two repositories, one for the backend and front end.
* 
<img width="1902" height="867" alt="Screenshot 2025-07-16 132220" src="https://github.com/user-attachments/assets/be3d23d8-45e3-4d04-b0ae-5351ff53bd3e" />

<img width="1902" height="874" alt="Screenshot 2025-07-16 132254" src="https://github.com/user-attachments/assets/f7cce2df-720e-446f-be55-00a2df951a65" />

* #### Successifully created the repositories in ECR
* 
<img width="1906" height="865" alt="Screenshot 2025-07-16 132440" src="https://github.com/user-attachments/assets/539421bc-5cbc-4664-99e7-7c9f0fd7f47d" />

* #### Login to ECR on the Jenkins server, using the ECR push command.
  
<img width="1907" height="891" alt="Screenshot 2025-07-16 132804" src="https://github.com/user-attachments/assets/ca0da184-9098-469a-a5e6-fed90130268c" />

<img width="1887" height="1015" alt="Screenshot 2025-07-16 133002" src="https://github.com/user-attachments/assets/42b7e57c-7e18-4b29-b00f-36d1a50e1e44" />


***


# 7a) Added Credentials in Jenkins

* #### I added a total of 7 Credentials.

* #### AWS

<img width="1866" height="903" alt="Screenshot 2025-07-16 134702" src="https://github.com/user-attachments/assets/17347937-ceec-49a1-97ce-7799051b4177" />

* #### Github

<img width="1798" height="801" alt="Screenshot 2025-07-16 140616" src="https://github.com/user-attachments/assets/085cd890-9189-41e3-8dff-9eff90e9eeda" />

* #### github

<img width="1891" height="854" alt="Screenshot 2025-07-16 142334" src="https://github.com/user-attachments/assets/e8872c9c-6376-408e-bab8-eb7a5f2b5e88" />

#### Sonarqube

<img width="1901" height="847" alt="Screenshot 2025-07-16 142601" src="https://github.com/user-attachments/assets/690a6ed0-dc63-4b42-8991-32913e188af1" />

#### ECR repo front end

<img width="1903" height="898" alt="Screenshot 2025-07-16 142833" src="https://github.com/user-attachments/assets/00e5b039-9cd9-4ebd-b386-926424bef6db" />

#### ECR repo back end

<img width="1820" height="842" alt="Screenshot 2025-07-16 143016" src="https://github.com/user-attachments/assets/37e4bdf6-b5e5-4595-a92a-d78163a95d6a" />

* ### I configured the installed plugins

* #### JDK
  
<img width="1794" height="681" alt="Screenshot 2025-07-16 144433" src="https://github.com/user-attachments/assets/2030f41a-b91b-4a84-a556-b5e35d047f58" />

* #### NodeJS
  
<img width="1651" height="766" alt="Screenshot 2025-07-16 144838" src="https://github.com/user-attachments/assets/cf0ab137-503a-49f0-9f45-4f8171cb695f" />

* #### Sonarqube Scanner

<img width="1699" height="651" alt="Screenshot 2025-07-16 144855" src="https://github.com/user-attachments/assets/34bf4b74-aa0c-42d1-a7fd-698bfea5490c" />

* #### Dependency-Check

<img width="1667" height="551" alt="Screenshot 2025-07-16 144958" src="https://github.com/user-attachments/assets/dc6c5287-c233-4384-9698-cf8e3465fb70" />

* #### Docker

<img width="1711" height="575" alt="Screenshot 2025-07-16 145133" src="https://github.com/user-attachments/assets/0d431402-ca41-43a6-b3c1-707d88df357d" />

* #### Sonar Installation

<img width="1585" height="669" alt="Screenshot 2025-07-16 145614" src="https://github.com/user-attachments/assets/6c10868c-35da-4ff1-a7ed-23e385114c0d" />


Provide the name as it is, then in the Server URL copy the sonarqube public IP (same as Jenkins) with port 9000 select the sonar token that we have added recently, and click on Apply & Save.

***

# 8) EKS Cluster Deployment


* #### I have created EKS Cluster using the below commands.
<img width="1915" height="971" alt="Screenshot 2025-07-16 145913" src="https://github.com/user-attachments/assets/87ba2dcc-954e-4aea-baff-2a6bd4157bfd" />

<img width="1904" height="938" alt="Screenshot 2025-07-16 152401" src="https://github.com/user-attachments/assets/50c6fa85-d8c3-4c5d-8623-ba9fad1e3178" />


* #### Once the cluster is ready, you can validate if the nodes are ready or not.

<img width="1894" height="936" alt="Screenshot 2025-07-16 152550" src="https://github.com/user-attachments/assets/0edc6f42-08f7-40c4-85f0-9f897a2d7c90" />

* #### Now, we will configure the Load Balancer on our EKS because our application will have an ingress controller.

<img width="1919" height="221" alt="Screenshot 2025-07-16 154439" src="https://github.com/user-attachments/assets/567a8847-bf3f-4dda-ad60-b4bee252d72d" />

* #### Download the policy for the LoadBalancer prerequisite.

<img width="1911" height="495" alt="Screenshot 2025-07-16 154624" src="https://github.com/user-attachments/assets/c4eae3d7-e7f9-44bf-95ff-36df6e9878b3" />

* #### Created OIDC Provider

<img width="1908" height="211" alt="Screenshot 2025-07-16 154929" src="https://github.com/user-attachments/assets/33d9bbc4-2f2f-469c-89ef-b1acf66ad73a" />

* #### Created a Service Account 

<img width="1893" height="616" alt="Screenshot 2025-07-16 155803" src="https://github.com/user-attachments/assets/f0a92454-58b9-4048-9dc1-2ef76fb09749" />


  ***

  
# 9) Prometheus and Grafana Installation and Configuration


* ####  Added Helm Stable Chart Repository

<img width="1907" height="598" alt="Screenshot 2025-07-16 161438" src="https://github.com/user-attachments/assets/788e5f0c-40c3-437f-b04d-50716c74bf56" />
  
* #### Added Prometheus Community Helm Repository

 <img width="1879" height="141" alt="Screenshot 2025-07-16 161524" src="https://github.com/user-attachments/assets/8f2ea759-eeff-43ec-860a-3a08da76c690" />

 * #### Added Helm EKS Chart Repository

 <img width="1465" height="86" alt="Screenshot 2025-07-16 160141" src="https://github.com/user-attachments/assets/af16013a-fb13-4d80-bcd0-2ab773093284" />

 * #### Created a Namespace for monitoring
<img width="1884" height="246" alt="Screenshot 2025-07-16 161632" src="https://github.com/user-attachments/assets/17e84af7-e626-4088-99f2-42d1d6191fe5" />

* #### Installed Prometheus with Grafana using Helm

 <img width="1919" height="641" alt="Screenshot 2025-07-16 161913" src="https://github.com/user-attachments/assets/e6256960-0b5f-43ca-85f5-139f9d45b61f" />

 * #### Verify Prometheus Installation

 <img width="1892" height="299" alt="Screenshot 2025-07-16 161958" src="https://github.com/user-attachments/assets/6407cc1e-8bda-4f3b-80f8-c5942f0effca" />

 * #### Check the Prometheus services:

 <img width="1908" height="550" alt="Screenshot 2025-07-16 162124" src="https://github.com/user-attachments/assets/a51cd347-c498-4bf9-afdc-d66285e87195" />

 * ####  Installed AWS loadbalancer

<img width="1905" height="821" alt="Screenshot 2025-07-16 160610" src="https://github.com/user-attachments/assets/32ddec39-d912-4985-963e-9b0048995b8a" />

* #### There are two ways to expose these services:

* #### NodePort
* #### LoadBalancer

* #### Exposing Prometheus via LoadBalancer:

<img width="1876" height="109" alt="Screenshot 2025-07-16 162556" src="https://github.com/user-attachments/assets/a7069edf-110e-4922-af6f-609df4852dd4" />

* #### Exposing Grafana via LoadBalancer:

<img width="1239" height="80" alt="Screenshot 2025-07-16 163225" src="https://github.com/user-attachments/assets/8bd573ff-2159-4116-95cb-9d15ebc647ce" />

<img width="1916" height="689" alt="Screenshot 2025-07-16 163447" src="https://github.com/user-attachments/assets/54b7ebf0-2b8f-4838-8f54-b7f90ea20f06" />

<img width="1895" height="480" alt="Screenshot 2025-07-16 160736" src="https://github.com/user-attachments/assets/fabefef5-ee78-41ea-a873-2b2d0a97a103" />


* #### Step 4: Verify Prometheus Installation

* #### Check the Prometheus pods:
<img width="1892" height="299" alt="Screenshot 2025-07-16 161958" src="https://github.com/user-attachments/assets/53106e1f-a1d2-4e0e-abaa-25a83f13b769" />



<img width="1890" height="568" alt="Screenshot 2025-07-16 162829" src="https://github.com/user-attachments/assets/997369e9-1b89-480d-a5b1-8f44324c80e3" />


* #### Step 6: Accessing Grafana

<img width="1908" height="680" alt="Screenshot 2025-07-16 164431" src="https://github.com/user-attachments/assets/262009b0-e6a7-4a9e-8e9d-b2360e0a0d67" />

<img width="1855" height="653" alt="Screenshot 2025-07-16 164517" src="https://github.com/user-attachments/assets/2faaa3ed-c317-42cf-9692-3905213de549" />

* #### The username will be admin and the password will be prom-operator for your Grafana LogIn.

<img width="1911" height="958" alt="Screenshot 2025-07-16 164536" src="https://github.com/user-attachments/assets/1956a57e-7377-4f96-a15c-92e8f3904d9d" />

<img width="1907" height="966" alt="Screenshot 2025-07-16 164551" src="https://github.com/user-attachments/assets/fa219ffd-f22e-4371-8c16-353d7c59d0c9" />

<img width="1910" height="894" alt="Screenshot 2025-07-16 164803" src="https://github.com/user-attachments/assets/1c6e1018-c116-4afb-8f91-32794e1ff5ed" />

<img width="1896" height="901" alt="Screenshot 2025-07-16 165211" src="https://github.com/user-attachments/assets/ba6f5e82-9a96-4a76-9a1d-3a9d188ef2bf" />

<img width="1907" height="978" alt="Screenshot 2025-07-16 165653" src="https://github.com/user-attachments/assets/de2a4a91-3a76-402e-8a2d-b7d34886af21" />

<img width="1889" height="890" alt="Screenshot 2025-07-16 170256" src="https://github.com/user-attachments/assets/b66745b6-f8ca-486e-9814-24bf6f51b9e4" />

<img width="1894" height="930" alt="Screenshot 2025-07-16 170445" src="https://github.com/user-attachments/assets/0a06665c-3e9a-4947-bed2-b576d1109993" />

<img width="1879" height="890" alt="Screenshot 2025-07-16 170648" src="https://github.com/user-attachments/assets/6327790c-078d-42c9-b085-595c44e8bc86" />

<img width="1912" height="909" alt="Screenshot 2025-07-16 170941" src="https://github.com/user-attachments/assets/9eb11db6-c629-413d-9a36-60161947f7b4" />


***


# 10) Jenkins Pipelines (Frontend & Backend)

<img width="1898" height="886" alt="Screenshot 2025-07-16 171212" src="https://github.com/user-attachments/assets/b9310bc0-a60c-416f-86a7-9abdd7452403" />

<img width="1864" height="889" alt="Screenshot 2025-07-16 172111" src="https://github.com/user-attachments/assets/9eee0b4e-893d-4116-98b0-94fd825f3646" />

<img width="1913" height="949" alt="Screenshot 2025-07-16 172746" src="https://github.com/user-attachments/assets/d59e1ad8-606e-400e-a407-384ae2605227" />

<img width="1878" height="915" alt="Screenshot 2025-07-17 091354" src="https://github.com/user-attachments/assets/0e11fa66-0421-4800-8796-194698ffe427" />

<img width="1611" height="640" alt="Screenshot 2025-07-17 100359" src="https://github.com/user-attachments/assets/4312a941-c171-4702-a429-6c611b6bbfaa" />

<img width="1689" height="671" alt="Screenshot 2025-07-17 100526" src="https://github.com/user-attachments/assets/03921efd-c1eb-4f9c-9ae9-ed1a59be67b1" />

<img width="1910" height="927" alt="Screenshot 2025-07-17 100741" src="https://github.com/user-attachments/assets/5588a6be-5a75-4a2e-84bc-8454ed2823b5" />

<img width="1803" height="732" alt="Screenshot 2025-07-17 100753" src="https://github.com/user-attachments/assets/6d18eb1a-bf50-4662-a34e-028ac5b94006" />


***


# 11) ArgoCD Installation & Application Deployment

* #### I installed argoCD.

* #### To do that, create a separate namespace for it and apply the argocd configuration for installation

<img width="1904" height="221" alt="Screenshot 2025-07-17 110709" src="https://github.com/user-attachments/assets/c403773f-5838-4c34-b103-cbfc8bd6a776" />

<img width="1892" height="975" alt="Screenshot 2025-07-17 111535" src="https://github.com/user-attachments/assets/34badcac-c5a5-479b-9fab-23e98eaa351f" />

* #### All pods must be running and we need to validate 

<img width="1904" height="295" alt="Screenshot 2025-07-17 111805" src="https://github.com/user-attachments/assets/a1bb025c-e237-49fc-ab77-6fabe2952a33" />

* #### Now, exposing the argoCD server as LoadBalancer

 <img width="1919" height="106" alt="Screenshot 2025-07-17 112612" src="https://github.com/user-attachments/assets/f6d572ec-ee8f-456a-ae1b-f0436f00fc16" />


* #### Now, we need to get the password for our argoCD server to perform the deployment. To do that, we have a pre-requisite which is jq. Installing it by the command below.
  
<img width="1893" height="1011" alt="Screenshot 2025-07-17 114616" src="https://github.com/user-attachments/assets/26ade10b-b963-41e7-b383-d02c6df80a93" />

<img width="1919" height="244" alt="Screenshot 2025-07-17 114726" src="https://github.com/user-attachments/assets/946eb856-7f9b-4960-8728-aefa177bda7c" />
  
<img width="1903" height="961" alt="Screenshot 2025-07-17 111612" src="https://github.com/user-attachments/assets/3f515c9d-a81a-4bf5-864f-181ccff3f6fb" />

<img width="1907" height="305" alt="Screenshot 2025-07-17 112324" src="https://github.com/user-attachments/assets/d22034b5-e431-497f-a333-78e7c3956c06" />

<img width="1732" height="34" alt="Screenshot 2025-07-17 112556" src="https://github.com/user-attachments/assets/66f143ff-96f1-4e9a-be43-463a768f5b01" />

<img width="1918" height="598" alt="Screenshot 2025-07-17 113122" src="https://github.com/user-attachments/assets/34b4339f-1277-40bb-a662-75da31261f56" />

* #### Next will deploy our Three-Tier Application using ArgoCD

* #### As our repository is private. So, we need to configure the Private Repository in ArgoCD.

* #### Then We have to set up database, backend, frontend , frontend ingress and backend-ingress applications.

<img width="1915" height="974" alt="Screenshot 2025-07-17 140434" src="https://github.com/user-attachments/assets/19cff984-d091-4f37-8997-59b94374b583" />

<img width="1904" height="974" alt="Screenshot 2025-07-17 113329" src="https://github.com/user-attachments/assets/89faaf1e-0dff-4b76-8d2f-6513414c6ac1" />

<img width="1919" height="975" alt="Screenshot 2025-07-17 114835" src="https://github.com/user-attachments/assets/d4e26648-bd14-4483-a22b-630f922116a3" />

<img width="1912" height="971" alt="Screenshot 2025-07-17 140332" src="https://github.com/user-attachments/assets/07be1929-ed64-4814-a5fa-9783a3da356e" />

<img width="1902" height="966" alt="Screenshot 2025-07-17 140404" src="https://github.com/user-attachments/assets/8e76239f-ad7f-470b-a826-67c701a8ee55" />

<img width="1900" height="943" alt="Screenshot 2025-07-17 114938" src="https://github.com/user-attachments/assets/c7b6bd9a-d676-4e2f-8f32-ec3312625ec3" />

<img width="1911" height="926" alt="Screenshot 2025-07-17 115527" src="https://github.com/user-attachments/assets/b24ca387-a282-470e-86ec-7630d446e68b" />

<img width="1892" height="980" alt="Screenshot 2025-07-17 120858" src="https://github.com/user-attachments/assets/95d04009-df18-4e26-892e-ee1e97dff0bd" />

<img width="1911" height="984" alt="Screenshot 2025-07-17 120944" src="https://github.com/user-attachments/assets/224930f9-f28b-4fa7-bf89-9cc82d9d6d2e" />
<img width="1912" height="969" alt="Screenshot 2025-07-17 135534" src="https://github.com/user-attachments/assets/f534f32f-2935-4a6c-8d0f-7d811849ba16" />

<img width="1916" height="885" alt="Screenshot 2025-07-17 135627" src="https://github.com/user-attachments/assets/1230dfcd-e5f6-433f-9588-4569d1ce407f" />

<img width="1914" height="970" alt="Screenshot 2025-07-17 135933" src="https://github.com/user-attachments/assets/e6b23702-f04e-4ca8-9364-8d6d0a9c58df" />

<img width="1914" height="930" alt="Screenshot 2025-07-17 122023" src="https://github.com/user-attachments/assets/1b9dbd8d-791f-4a4b-91c5-7aa114eedc04" />

* #### Pipeline overview

<img width="1911" height="886" alt="Screenshot 2025-07-17 123732" src="https://github.com/user-attachments/assets/ee8c8e01-8693-4fda-9656-1d232520bfbe" />




