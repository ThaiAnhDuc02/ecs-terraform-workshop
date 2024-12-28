+++
title = "Monitoring"
date = 2024
weight = 8
chapter = false
pre = "<b>8. </b>"
+++

#### Configure Container Insights (CloudWatch)

In this section, we’ll need to configure some settings before using Container Insights. Container Insights is a service that allows us to monitor metrics such as CPU usage, Network activity, and more, giving insight into user activity over a certain period.

Combined with CloudWatch, we can view logs sent from Containers in groups, usually with the prefix /ecs/*. This gives a more comprehensive view of applications in the system—how they're running, any alerts, and the ability to read logs for troubleshooting errors or investigating unusual traffic when the system is compromised.

- On the **ECS** console page, in the right-hand menu, select **Account settings**.
- Choose **Update**.

![image](/images/8-monitoring/8.1.png)

- Select **Container Insights**.
- Click **Save changes**.

![image](/images/8-monitoring/8.2.png)

- Complete the Container Insights configuration.

![image](/images/8-monitoring/8.3.png)

#### Observing Metrics with Performance Monitoring

- Go back to **Clusters**.
- Select **Metrics**.
- Click on **View Container Insights** to observe metrics.

![image](/images/8-monitoring/8.4.png)

- View the metrics with **ECS**.

![image](/images/8-monitoring/8.5.png)

To switch to observing **Task definitions**, follow these steps:

- In the highlighted section, change it to **ECS Tasks** to monitor events there.

![image](/images/8-monitoring/8.6.png)

Similarly, to view events for ECS Service:

- In the highlighted section, change it to **ECS Service** to monitor those events.

![image](/images/8-monitoring/8.7.png)

#### Observing Metrics with Container Map

Here, you can view which **Containers**, **Tasks**, and **Services** are running within the **Cluster** you’ve deployed, with greater specificity.

- Change **Performance Monitoring** to **Container Map**.

![image](/images/8-monitoring/8.8.png)

You’ll see a new interface showing how a **Cluster** manages related resources like **Services** and **Tasks**. Note that metrics within a Task differ from those within a **Service**, as **Services** directly manage **Tasks**, meaning Task metrics are also applicable to Services.

![image](/images/8-monitoring/8.9.png)

Here, you can also view details for each service.

- Click on **Service backend**.
- Select **Metrics**.

![image](/images/8-monitoring/8.10.png)

Similarly, you can view Task definitions:

- Click on **Task fe**.
- Choose **Metrics**.

![image](/images/8-monitoring/8.11.png)

#### Observing Metrics with Resources

- Change **Container Map** to **Resources**.

![image](/images/8-monitoring/8.12.png)

Here, you’ll see a list of created events, allowing you to select and monitor each service.

![image](/images/8-monitoring/8.13.png)

{{% notice tip %}}
We have completed configuration and monitoring with Container Insights, but AWS provides other monitoring and tracking services beyond Container Insights, including third-party services.
{{% /notice %}}

**Congratulations on completing this Workshop!**
