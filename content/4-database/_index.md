+++
title = "Add Database to RDS"
date = 2024
weight = 4
chapter = false
pre = "<b>4. </b>"
+++

#### Connect to EC2 Instance

First, I need to access the instance created by Terraform and connect to it to add data to RDS.

- Search for `ECS Instance` in the AWS console.
- Select the name of the instance created and click **Connect**.

![image](/images/4-rds/4.1.png)

- Choose **SSH client**.
- Copy the path as shown.

![image](/images/4-rds/4.2.png)

- Paste it into your VS Code and configure the path for the **Key pair** you saved.
- Successfully connected.

![image](/images/4-rds/4.3.png)

#### Add Database

{{% notice note %}}
Since my Terraform configuration has already set up the dependencies and includes a sample database, adding data to RDS will be easier.
{{% /notice %}}

Now, we will navigate to the pre-set directory and add the absolute path for the database here.

- We will use the following command:

```
cd ./aws-fcj-container-app/database/
echo $PWD/init.sql
```

![image](/images/4-rds/4.4.png)

Next, we need to log in to RDS to add the data from that path.

- Copy the RDS Endpoint.
- Use that endpoint in the following command:

```
mysql -h "rds-endpoint" -u "name-user" -p
```

![image](/images/4-rds/4.5.png)

- Paste the command into the virtual machine and enter the password to connect to RDS.
- Paste the path with data into the connected RDS.

```
source /home/ubuntu/aws-fcj-container-app/database/init.sql
```

![image](/images/4-rds/4.6.png)

- Data added successfully.

![image](/images/4-rds/4.7.png)

- Use some commands to check the database.

```
SHOW DATABASES;
USE fcjresbar;
SELECT * FROM Clients;
```

![image](/images/4-rds/4.8.png)