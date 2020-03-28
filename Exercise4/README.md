# Load Tests on Azure
In this exercise, you will learn how to run real load tests using JMeter on Azure infrastructure.

## Exercise
Create two virtual machines with JMeter image and run test plan created in exercise no 3.

### Steps
1. Login in to Azure portal, click on Create Resource and type in search bar jmeter. You should be able to find 
**Load Tester (standalone) Powered by Apache JMeter™**.

![Alt text](JMeter.png?raw=true "Create JMeter VM")

2. Click on **Start with a pre-set configuration**. And choose below configuration:

![Alt text](Preset.png?raw=true "Preset")

3. Create VM using these settings:

![Alt text](VmOptions.png?raw=true "VmOptions")

and click **Create+Review**

**If you don't know how to generate ssh-key use google!**

4. Create another VM using the same settings but instead of creating another network use network settings from first VM like so:

![Alt text](NetworkConfig.png?raw=true "NetworkConfig")

and click **Create+Review**

5. Allow to communicate with Virtual Machine using port 1099. Add network rule as below:

![Alt text](NetworkRule.png?raw=true "NetworkRule")

in newly created Virtual Machines with JMeter

6. Open terminal and login in to one newly created VM like so:

```console
ssh vm_user@vm_ip

```
where:
* vm_user - is user provided on vm settings page in ssh section
* vm_ip - virtual machine ip. You can find it in Overview section in Public IP address

7. Create RMI key using script:

```console
/usr/local/jmeter/bin/create-rmi-keystore.sh
```

the script will ask you about a few things you can enter what you want.
It will ask you to provide a password leave it blank.

8. Script should generate rmi_keystore.jks file in this location /usr/local/jmeter/bin/. Please check it.
9. This rmi_keystore.jks file must be copied on second VM with JMeter. You can copy this file on your local computer and from local computer to second VM like so:

```console
scp /usr/local/jmeter/bin/rmi_keystore.jks user@ip:/home/user/
scp /home/user/rmi_keystore.jks vm_user2:vm_ip2:/usr/local/jmeter/bin/
````
where:
* user - user of your local machine
* ip - ip of your local machine
* vm_user2 - is user provided on vm settings page in ssh section
* vm_ip2 - virtual machine ip. You can find it in Overview section in Public IP address

Of course, you can directly copy this file into the second VM but you need to generate ssh-key for the first VM and add public key in Azure portal to the second VM.

10. Open another terminal. Login into second VM and run jmeter-server like so:

```console
/usr/local/jmeter/bin/jmeter-server
```

11. Copy your test plan on the first VM using scp command into /usr/local/jmeter/bin/.
12. From first VM from type:

```console
/usr/local/jmeter/bin/jmeter -n -t testplan -e -o report_dir -R vm_ip2
````

where:
* testplan - test plan name it should have extension .jmx eg. testplan.jmx.
* report_dir - the path where to store JMeter report eg. ~/report.
               **Warning:** folder should be created before the test and should be empty.
* vm_ip2 - ip of the second virtual machine where jmeter-server is running.

13. After the test ends in report_dir you should have the whole report.
