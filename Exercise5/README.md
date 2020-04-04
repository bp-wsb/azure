# Scaling application on Azure
In this exercise, you will learn how to scale vertical and horizontal application.

## Exercise
Deploy your application and create rules to scale it.

### Steps
1. Login in to Azure portal.
2. Go to application and click on **Scale Up**. Change plan as below:

![Alt text](scale_up.png?raw=true "ScaleUp")

Now you have possibility to scale horizontal your app.

3. Go to **Scale Out** and choose **Custom autoscale**.

4. Create two conditions: 

![Alt text](autoscale.png?raw=true "Autoscale")

5. The first condition will increase number of server instance by 1 when CPU load will be >= 70%

![Alt text](criterium_1.png?raw=true "Criterium1")

6. The second condition will decrease the number of server instance by 1 when CPU load will be <= 30%.

![Alt text](criterium_2.png?raw=true "Criterium2")

This will prevent paying for servers that are not needed anymore.

7. Prepare load tests environment as in exercise 4.
8. Run load tests and check if scaling works properly by comparing measurements fro previous lessons.
