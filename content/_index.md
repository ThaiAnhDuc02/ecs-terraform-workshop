+++
title = "Infrastructure Deployment with Terraform Integrated with GitHub Actions"
date = 2024
weight = 1
chapter = false
+++

# Infrastructure Terraform Integrated with GitHub Actions

#### Architecture

![1](./images/)

#### Workflow

To complete this Workshop, we will follow a simple process as outlined below:

- Write the Terraform infrastructure code for the pre-defined system.
- Use commands to deploy the infrastructure on the AWS console.
- Deploy ECS Service on the pre-created infrastructure.
- Set up CI/CD to automate the deployment process.
- Create Monitoring to observe and manage the system.

This process ensures that the deployment of infrastructure, services, and CI/CD is fully automated, providing high efficiency and comprehensive control over the AWS-based system.


#### Table of Contents

1. [Introduction](1-introduce/)
2. [Preparation](2-preparation/)
3. [Terraform Infrastructure](3-terraform/)
4. [Add Database to RDS](4-database/)
5. [Create ECS Service](5-ecs-service/)
6. [Verify Results](6-result/)
7. [CI/CD Deployment with GitHub Actions](7-cicd-github/)
8. [Monitoring](8-monitoring/)
9. [Resource Cleanup](9-clean-up/)