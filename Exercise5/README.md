# Scaling application on Azure
In this exercise, you will learn how to scale vertical and horizontal application.

## Exercise
Deploy your application and create rules to scale it.

### Steps
1. Login in to Azure portal.
2. Go to application and click on **Scale Up**. Change plan as below:

![Alt text](scale_up.png?raw=true "ScaleUp")

Now you have possibility to scale horizontal your app.

3. Go to **Scale Out** and choose **Custom autoscale**:

![Alt text](autoscale.png?raw=true "Autoscale")

4. Setup **Auto created scale condition** like on the screen

![Alt text](criterium_1.png?raw=true "Criterium1")

5. Create another condition clicking on **Add scale condition** and set up as below:

![Alt text](criterium_2.png?raw=true "Criterium2")

6. Prepare load tests environment as in exercise 4.
7. Run load tests and check if scaling works properly by comparing measurements fro previous lessons.