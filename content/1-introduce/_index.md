+++
title = "Introduction"
date = 2024
weight = 1
chapter = false
pre = "<b>1. </b>"
+++

#### Context

Why this Workshop?

In practice, deploying **AWS** infrastructure with **Containers** can often be complex and time-consuming. Manual processes are prone to configuration errors, difficult to manage, and can lead to unnecessary resource waste when issues arise. **Terraform** addresses these challenges by automating the creation and management of infrastructure, making the process faster and easier. Combined with **CI/CD**, deployment becomes more efficient and trackable, helping businesses reduce risk and improve system management effectiveness.

This process offers clear benefits:

- **Time and Cost Savings**: Automation reduces manual work and increases work efficiency.
- **High Reliability**: Services are deployed consistently, minimizing configuration errors.
- **Flexible Scalability**: The infrastructure can easily scale up or down according to demand, optimizing operational costs.
- **Quick Response to Changes**: CI/CD enables faster product improvement and system updates, better meeting market demands.

Thanks to this process, the company not only meets expansion needs but also optimizes service quality, increasing competitiveness and enhancing customer satisfaction.

#### What is Terraform?

![Terraform](/images/1-account-setup/terraform.jpg)

**Terraform** is an open-source tool developed by **HashiCorp** used for managing infrastructure (**Infrastructure as Code - IaC**). It enables users to define and deploy infrastructure via code, automating the creation, updating, and management of resources such as servers, databases, networks, and other services on cloud platforms like AWS, Azure, Google Cloud, as well as on-premises systems.

Key features of Terraform:
- **Infrastructure as Code (IaC)**: Infrastructure is described in code, allowing for version control, easy sharing, and backup, similar to managing an application's source code.
- **Automated Deployment and Configuration**: With Terraform, users can deploy or change resources in bulk with a single command, saving time and reducing manual errors.
- **Platform Independence**: Terraform supports multiple cloud providers, making it easy to deploy multi-cloud infrastructure or switch between platforms without changing tools.
- **Lifecycle Management of Resources**: Terraform not only creates but also manages the entire resource lifecycle, including updates, modifications, and deletions as needed.
- **Modularity and Extensibility**: Terraform allows infrastructure to be divided into modules, making management flexible, easy to maintain, and scalable as the system grows.

With these advantages, Terraform simplifies infrastructure management, making changes safe, controllable, and easy to deploy on a large scale.

#### GitHub Actions CI/CD

**GitHub Actions** is an integrated automation service on GitHub, helping to automate the software development workflow from code testing to application deployment, making it easy to set up CI/CD (Continuous Integration/Continuous Deployment).

1. **Continuous Integration (CI)**
   - Automatic Build and Test: Automatically builds and tests code whenever there are changes, helping to detect errors early.
   - Workflows: Defines workflows to automatically perform testing, building, and releasing code on events like new pull requests or commits.
2. **Continuous Deployment (CD)**
   - Automated Deployment: Supports automatic application deployment to environments like staging or production when code is approved.
   - Service Integration: Easily integrates with services like AWS, Azure, and Google Cloud.
3. **Key Features**
   - Customization: Create custom actions or use actions from the GitHub Marketplace.
   - User-Friendly Interface: Easily set up and manage workflows without deep scripting knowledge.
   - Resource Management: Monitors workflow status and provides detailed information about the testing and deployment process.
4. **Benefits**
   - Time-Saving: Reduces repetitive work for developers.
   - Improved Code Quality: Enhances software quality through frequent testing and deployment.
   - Flexibility: Easily adjust CI/CD processes to suit project needs.

#### Monitoring with CloudWatch Container Insights

**CloudWatch Container Insights** is a feature in **AWS CloudWatch** that provides monitoring and analytics capabilities for containers running on Amazon ECS (Elastic Container Service) and EKS (Elastic Kubernetes Service). Below are some highlights of Container Insights:

- **Performance Monitoring**: Container Insights allows you to track key performance metrics such as CPU, memory, and network for each container, helping to detect issues early and optimize application performance.
- **Container Health Statistics**: You can view detailed information about the operational status of containers, including their state (running, stopped, error) and other metrics like runtime and replica count.
- **AWS Integration**: Container Insights can be easily integrated with other AWS services, allowing you to build comprehensive monitoring solutions and create custom reports based on container metrics.
- **Visual Dashboard**: AWS provides visual dashboards that make it easy to monitor the status and performance of containers, along with the ability to set alerts when issues arise.

{{% notice tip %}}
Before starting the Workshop, we recommend spending a bit of time getting familiar with the contents you’ll be working on. Now, let’s dive in and explore each step of the Workshop. Wishing you a smooth experience and the best results!
{{% /notice %}}
