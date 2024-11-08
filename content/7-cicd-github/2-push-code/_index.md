+++
title = "Create a New Project and Push Code"
date = 2024
weight = 2
chapter = false
pre = "<b>7.2. </b>"
+++

#### Create a New Repository

This repository will be used to run GitHub Actions.

- First, log into your GitHub account.
- Select **Repositories**.
- Choose **New**.

![image](/images/7-cicd/7.2.1.png)

- Enter the repository name: `terraform-cicd`
- Enter a description: `Use for CI/CD`
- Select **Public**.
- Click **Create repository**.

![image](/images/7-cicd/7.2.2.png)

- Repository creation is complete.

![image](/images/7-cicd/7.2.3.png)

#### Push Code

Access the virtual machine where you have cloned and edited your code.

- Use the command to **set up remote repo**.
- Check if **remote** setup was successful.

```bash
git remote set-url origin "GitHub repo link"
git remote -v
```

![image](/images/7-cicd/7.2.4.png)

- Use the following commands to push your code to the newly created repository.

```
git add .
git commit -m "Fist commit"
git branch -M main
git push -u origin main
```

![image](/images/7-cicd/7.2.5.png)

- Verify in the GitHub repository to see if the code has been successfully pushed.

![image](/images/7-cicd/7.2.6.png)
