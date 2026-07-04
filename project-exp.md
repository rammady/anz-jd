Question 1: Walk me through your project.

Answer:

The project I worked on was an Enterprise Identity and Access Management platform used internally across the organization.

Its primary purpose was to provide centralized authentication and authorization services for various internal business applications. Whenever an employee logged into an application, requested access to a service, or performed identity verification, the request was processed through this platform.

Since hundreds of applications depended on it, the platform was considered business critical. Any downtime would impact employee login, application access, and business operations.

From an infrastructure perspective, the platform was hosted on AWS. We used Amazon EKS to run our containerized microservices. Traffic first reached an Application Load Balancer, which routed requests to Kubernetes Ingress and then to the appropriate microservices running inside the EKS cluster.

The application images were stored in Amazon ECR. Infrastructure such as VPCs, subnets, IAM roles, EKS clusters, security groups, and supporting AWS resources were provisioned using Terraform. Configuration management and operational automation activities, such as package installation, Linux configuration, and patching, were handled through Ansible.

For continuous integration, we used Jenkins. Developers pushed code to GitHub, Jenkins built the application, created Docker images, pushed them to ECR, and updated the deployment manifests stored in Git. ArgoCD continuously monitored the Git repository and automatically synchronized changes to the Kubernetes cluster following GitOps principles.

For observability, we used Prometheus for metrics collection, Grafana for dashboards, Splunk for centralized log analysis, and CloudWatch for AWS infrastructure monitoring and alarms.

My primary responsibilities were on the DevOps and Site Reliability Engineering side. I was responsible for infrastructure provisioning using Terraform, maintaining Jenkins pipelines, supporting Kubernetes deployments, monitoring production environments, responding to incidents, performing root cause analysis, maintaining runbooks, improving alert quality, and collaborating with application teams to improve platform reliability and reduce operational issues.

I also participated in on-call support, production releases, infrastructure changes, and post-incident reviews. My focus was always to improve platform stability, reduce MTTR, automate repetitive operational work, and ensure that deployments were reliable and repeatable.
