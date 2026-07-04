## Project Name
**Enterprise Identity & Access Reliability Platform**

## Business Context
The project supported an enterprise Identity and Access Management platform used by internal business applications for:

-  User authentication 
-  LDAP-based directory lookup 
-  MFA validation 
-  Access policy enforcement 
-  Internal application login 
Because many applications depended on this platform, any outage could impact employee login, business application access, and support operations.

Mousumi’s team was responsible for **platform reliability, deployment automation, monitoring, infrastructure provisioning, incident response, and operational stability**, not core application development.



**Architecture**

## High-Level Architecture
Users / Internal Apps
 → AWS ALB
 → EKS Ingress Controller
 → Kubernetes Services
 → IAM / Auth Microservices
 → LDAP / Directory Backend
 → Logs to Splunk
 → Metrics to Prometheus / Grafana
 → Infra metrics to CloudWatch





## AWS Components
-  VPC with public and private subnets 
-  ALB in public subnet 
-  EKS worker nodes in private subnet 
-  NAT Gateway for outbound traffic 
-  IAM roles for access control 
-  ECR for Docker images 
-  S3 for logs/artifacts/backups 
-  CloudWatch for AWS infrastructure metrics



**Role and Responsibilities**

My role was mainly DevOps/SRE. I was not writing application business logic. I was responsible for keeping the platform reliable, automating deployments, maintaining monitoring dashboards, handling production incidents, improving alerting, managing infrastructure changes through Terraform, and supporting Kubernetes-based deployments on AWS EKS.



## Daily Responsibilities
-  Monitor production alerts from Prometheus, Grafana, Splunk, and CloudWatch 
-  Troubleshoot pod failures, high CPU, memory issues, and application latency 
-  Support Jenkins pipeline failures 
-  Review ArgoCD sync status and deployment health 
-  Create or modify Terraform code for AWS infrastructure changes 
-  Use Ansible for Linux configuration, patching, agent installation, and operational tasks 
-  Participate in incident calls and RCA 
-  Maintain runbooks and post-incident documentation 
-  Support capacity planning and right-sizing 
-  Coordinate changes using ServiceNow/Jira




**CI/CD Flow You Can Explain**

## Jenkins CI Pipeline
Developer commits code
 → Jenkins pipeline starts
 → Checkout from Git
 → Build application(Java project, then Maven)
 → Run basic tests (Junit for unit testing)
 → Build Docker image
 → Scan image if configured- (Trivy)
 → Push image to Amazon ECR
 → Update Kubernetes manifest/image tag repo
 → ArgoCD detects Git change
 → ArgoCD deploys to EKS

SAST, DAST , DvSecOps 



## ArgoCD CD Flow
-  ArgoCD continuously compares Git desired state with EKS actual state 
-  If manifest changes, ArgoCD syncs deployment 
-  It deploys updated image to Kubernetes 
-  Rollback can be done by reverting Git commit or syncing previous version 
-  Health status is checked through Kubernetes readiness/liveness probes
 explanation:

>  “Jenkins was used for CI. ArgoCD was used for CD. Jenkins built and pushed Docker images. ArgoCD deployed the approved Kubernetes manifests to EKS using GitOps.”







# Monitoring Strategy
## Prometheus
Used for:

-  Pod CPU/memory 
-  Container restarts 
-  Node health 
-  Application availability 
-  HTTP error rate 
-  Latency 
-  Kubernetes object health 
## Grafana
Dashboards for:

-  Cluster health 
-  Namespace health 
-  Pod restart count 
-  CPU and memory trend 
-  API latency 
-  Login/authentication success rate 
-  Error rate


## CloudWatch
Used for:

-  EC2/EKS node metrics 
-  ALB request count 
-  ALB 4xx/5xx 
-  Target response time 
-  AWS infrastructure-level alarms 


**Realistic Production Incidents**

Incident 1: Authentication Latency After Deployment

**Question:** Tell me about a production issue you handled.

Answer:

After one release, we noticed increased login latency. Grafana showed high response time for the authentication service, and Prometheus showed pod CPU going above 85%. Splunk logs showed repeated LDAP connection timeout messages. We checked the recent deployment in ArgoCD and found that a connection pool configuration had changed. We rolled back the deployment through GitOps, increased replicas temporarily, and service latency came back to normal. Later, we added better alerts for LDAP timeout rate and updated the runbook.







## Incident 2: Kubernetes Pod Restart Issue
>  “We received alerts for frequent pod restarts in one namespace. Using kubectl describe and logs, we found memory limit breaches. Prometheus confirmed memory usage was gradually increasing. We increased memory limits temporarily, informed the application team, and later adjusted resource requests/limits based on observed usage. We also added a Grafana panel for restart trends.”



## Incident 3: Jenkins Pipeline Deployment Failure
>  “One deployment failed because the Docker image was pushed successfully to ECR, but ArgoCD was not syncing the latest manifest. We found the image tag update step in Jenkins had failed due to Git permission issues. We fixed the credential issue, re-ran the pipeline, and added validation so the pipeline fails clearly if the manifest repo update does not happen.”



git checkout -b branch 







# Switch branch 

git checkout main

or 

git switch main

# swich branch 

it checkout -b feature/test-insecure

# swtich to main branch 

git checkout main

OR

git switch main

# check your current branch 

git branch 

# check all the available branches 

git branch -a 

# Create. anew branch and swtich to it 

 git checkout -b feature/test-insecure

means:

- `**git checkout -b**`  → Create a new branch and switch to it immediately.
- `**feature/test-insecure**`  → The name of the new branch.


