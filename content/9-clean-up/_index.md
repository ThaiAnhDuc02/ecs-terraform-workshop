+++
title = "Resource Cleanup"
date = 2024
weight = 9
chapter = false
pre = "<b>9. </b>"
+++

#### Cleaning Up on the AWS Console

First, you need to access the AWS console to delete the services you previously created manually.

- In the **console**, search for **CloudFormation**.
- Select **Stacks**.
- Choose the 2 **Services** you created and click **Delete**.

![image](/images/9-clear/9.1.png)

- Click **Delete**.

![image](/images/9-clear/9.2.png)

- Wait approximately 5 to 10 minutes for the deletion process to complete.

![image](/images/9-clear/9.3.png)

- Go back to the ECS cluster to check if the service has been deleted.

![image](/images/9-clear/9.4.png)

#### Cleaning Up with Terraform Commands

{{% notice note %}}
Since the resources in the infrastructure were created by **Terraform**, you can conveniently delete all resources with a single command instead of manually removing each one.
{{% /notice %}}

Now, go back to the location where you initially deployed the infrastructure with Terraform.

- Use the command below to delete resources.

```
terraform destroy
```


![image](/images/9-clear/9.5.png)

- Type `yes` to confirm.

![image](/images/9-clear/9.6.png)

- Wait approximately 15 to 20 minutes for all resources to be deleted.

![image](/images/9-clear/9.7.png)

- After a successful deletion, return to the AWS console to verify that all resources have been removed.

![image](/images/9-clear/9.8.png)
