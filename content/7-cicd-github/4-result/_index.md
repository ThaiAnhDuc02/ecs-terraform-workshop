+++
title = "Check Results"
date = 2021
weight = 4
chapter = false
pre = "<b>7.4. </b>"
+++

#### Create a Tag

To trigger the CI/CD pipeline, we need to create a new tag for the code.

- Go to your **repository**.
- Select **Tags**.

![image](/images/7-cicd/7.4.1.png)

- Choose **Releases**.
- Click **Draft a new release**.

![image](/images/7-cicd/7.4.2.png)

- Enter a new tag name: `v1.0.4`.
- Click **Create new tag**.

![image](/images/7-cicd/7.4.3.png)

- Select **Publish release** to confirm.

![image](/images/7-cicd/7.4.4.png)

#### Check Results

To monitor the CI/CD process, follow these steps:

- Go to **Actions**.
- Select the name of your workflow.

![image](/images/7-cicd/7.4.5.png)

- View the **CI/CD** process for both **backend** and **frontend** here.
- If there is an error, check the **logs** below.

![image](/images/7-cicd/7.4.6.png)

After CI/CD has successfully run, go to the AWS Console to check if components such as Task Definitions and Services have been updated.

- Go to **Task definitions** to see if a new task has been created.
- First, check the **Backend** task.

![image](/images/7-cicd/7.4.7.png)

- Next, check the **frontend** task.

![image](/images/7-cicd/7.4.8.png)

- Verify that the **Service** is being updated.

![image](/images/7-cicd/7.4.9.png)

Once everything is complete, go back to the DNS of the Load Balancer to check if your updates have been applied.

- Reload the current page.

![image](/images/7-cicd/7.4.10.png)
