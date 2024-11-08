+++
title = "Infrastructure Introduction"
date = 2024
weight = 1
chapter = false
pre = "<b>3.1. </b>"
+++

#### Terraform Infrastructure

As previously introduced, Terraform allows for the automated and organized configuration of cloud infrastructure on AWS. The template prepared below already includes code for infrastructure deployment, with the structure outlined as follows:

- There are 4 main files used throughout the configuration and setup of each service:
  - **terraform.tf**: Configures the provider, which is a basic file and typically requires minimal changes.
  - **variable.tf**: Stores variables, making it easy to adjust values for each deployment.
  - **main.tf**: The main file to run programs and services for the configured infrastructure.
  - **output.tf**: Outputs the values of resources post-deployment, allowing these values to be reused for other purposes.

- The **modules** folder will contain the configuration of each service.
- The **.tf** files outside the **modules** folder combine these services, enabling synchronized deployment and optimizing the process.
- Template link: https://github.com/LyHoangViet/Terraform-DoAn.git

{{% notice tip %}}
To better understand the sections in the provided template, I recommend reviewing the Terraform course on [KodeKloud](https://learn.kodekloud.com/courses/terraform-basics-training-course) and creating your own infrastructure to gain additional insight into this template.
{{% /notice %}}

![image](/images/3-terraform/3.1.1.png)

- You can read the README file to learn more about this infrastructure.
- Install the necessary tools as instructed.

![image](/images/3-terraform/3.1.2.png)

- Adjust the variables in the configuration file on your local machine.

![image](/images/3-terraform/3.1.3.png)

- How to deploy using Terraform commands.

![image](/images/3-terraform/3.1.4.png)
