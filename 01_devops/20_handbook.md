1. DevOps  
  
**DevOps** is software engineering culture and practice that aims at unifying software development and software operations.  
**DevOps** aims at shorter development cycles.  
That also means that you are **increasing** the deployment **frequency** and more dependable releases in close alignment with business objectors.  
  
**DevOps practices:**
- continuous integration
- server orchestration
- monitoring
- ...
Deliver features frequently (Goal: speed) VS Maintain Stability (Goal: stability)  
  
Automation leads to Consistency:
- Automated Builds
- Automated Integration
- Automated Testing
- Automated Deployment
  
Parallel Processing &&& Monitoring  
  
Book: DevOps HandBook (Gene Kim, Patric Debois)  
  
2. Build automation  
**Tools:** Jenkins, Maven, Gradle, Bazel, Make, CMake  
Build automation is independent of an IDE  
Should be machine agnostic. BA is fast, consistent, repeatable & portable, reliable  
  
3. Continuous Integration  
Resolves code / merge conflicts problem
Benefits of CI:
- Ensures everyone's changes are integrated
- Catch bugs
- Reduce merge conflicts
CI Tools: Jenkinsc(Java Servlet Web App), CircleCI, GitLab Ci, ZUUL CI, Bamboo (atlassian)  
Automated build: Automated tests are running on the code for each merge -> Automatic notifications for codeowners  
Detect errors earlier in the development lifecycle  
CI also makes frequent releases possible  
  
4. Continuous Deployment  
Continuous Deployment is a practice where every change that is passing through all the stages of the production pipeline is released to customer  
Continuous Deployment is a practice frequently deploying small code changes to prod  
  
5. Continuous Delivery
Continuous Delivery - is a process to keep the code ready for deployment  
  
6. Infrastructure as a Code
Managing and provisioning infrastructure using Code  
Use Code to deploy infrastructure of any size  
Tools: Ansible (Declarative configuration, doesn't require centralized server, doesn't require agents -> py, ssh, idempotency)  
Goal: to avoid human errors, consistent deployment, reusability, scalability of the Code  
Makes Infrastructeure Self-Documneted  
  
7. Configuration Management

Doing the changes in a maintainable way & minimizing configuration drift
Maintain and change the state of various pieces of infrastructure in a consistent way
Tools: Ansible ( Declarative configuration), Puppet (Declarative configuration), Chef (procedural configuration), SALT (Declarative configuration)
  
8. Monitoring
Quickly respond to problems, collect system metrics
Represent data in presentable manner
Assists in troubleshooting
Tools Infrastructure Monitoring: Sensu, New relic (SAAS), ELK
Tools App Performance: APPDYNAMICS, Elastic Stack
  
9. Microservices
Microservices architecture - collection of small but loosely coupled services (VS Monolithic Architecture) - crucial for large and complex apps
Microservices interact with each other and with application overall using a stable well defined APIs
Microservices are modular, flexible
Microservices offer optimized stability
  
10. Tools for Virtualization and Containerization
Hypervisor is a program that runs on the bare physical metal and allows to manage virtual machines
Virtualization Tools: VMware, hyper-v, Xen server
Containerization Tools: Docker
Orchestration Tools: Docker swarm, Kubernetes, ZooKeeper, Terraform (IaaS - infrastructure as a service)
  
11. Cloud
IaaS - infrastructure as a service
The Cloud provider typically provides you with bare operating system
AWS (EC2)
Google Cloud, Azure
PAAS - platform as a service (Heroku, App Engine)
SAAS - software as a service (Gmail, office 365)
FAAS - function as a service (AWS Lambda, Azure Functions, Google Cloud Functions)
