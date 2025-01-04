# Microsoft Sentinel Playbooks

## Objective

The Microsoft Sentinel Playbooks project aims to implement a Linux honeypot called "cowrie" using Microsoft Azure and lure attackers to reveal their tactics, techniques, and procedures (TTP's). If you are lucky they might even drop their toolkit and you can perform basic malware analysis!

### Skills Learned 

Setup and Configuration: Understanding the installation of VM's using Microsoft Azure
FILL IN THE REST AFTER COMPLETE

### Tools Used

- Microsoft Azure:
- Microsoft Sentinel:


### Step-By-Step Guide

1) To begin we will need to head over to https://portal.azure.com and sign up for an account. If you haven't used Azure before you will have a 200$ free credit for 30 days.

![1](https://github.com/user-attachments/assets/b9973843-f565-4dd4-a26e-d66d5e2f77cd)

*Ref 1: Create Azure Account*

2) Once you are signed in and have your subscription ready to go, the next thing to do is enable your subscription for monitoring. To do that you must register for Microsoft Insights by first clicking the new subscription you just created. Then at the bottom left select Resource Providers and filter by the provider: Microsoft.Insights

![1](https://github.com/user-attachments/assets/dfa1bfaa-2538-47da-9013-967108f238fa)
![1](https://github.com/user-attachments/assets/483216a4-f6dd-466e-8b37-b5ae41709db5)
*Ref 2: Subscription*

3) Select Microsoft.Insight and then click Register.

![1](https://github.com/user-attachments/assets/f7483583-f3cc-4b68-a7da-1ed46842e253)

*Ref 3:Register*

4) Now that our subscription is ready to go we can now begin creating our first Resource Group which is essentially a container for all your resources like virtual machines, network adapters, etc. To create a Resource Group simply click on the home button in the top left corner and under Azure Services you will see Resouce Groups. If you don't see it simply type in "Resource Groups" in the search bar. 

![1](https://github.com/user-attachments/assets/47feffa2-5f5b-4a66-8c30-3551f5ae6716)

*Ref 4: Resource Groups*

5) Now click on Create in the top left or middle of the screen to create our first Resource Group. Give your Resource Group a name, select the region closest to you then click on Review + Create in the bottom left and Create again after validation passes.

![1](https://github.com/user-attachments/assets/af68ffe5-0834-4384-b298-965ad03fb483)
![2](https://github.com/user-attachments/assets/4cff37b5-7b4f-4b91-9593-aa56cc14d27d)

*Ref 5: Create Resource Groups*

6) Now that we have our Resource Group created the next thing we want to do is create our virtual machine. To do that search "Virtual Machines" in the search bar and click on Virtual Machines. Just like before click on Create in the top left or middle of the screen and then select Azure virtual machine. In this project we will have a total of two virtual machines, one is going to be acting as our Linux HoneyPot Server using cowrie. The second one is going to be acting as a Windows Server machine with remote desktop aka RDP exposed to the public.

![1](https://github.com/user-attachments/assets/fa0430fa-00c5-4263-bca5-cb05cc2a5ca8)
![2](https://github.com/user-attachments/assets/1ecb9106-af65-45cf-ac3d-5325d80cfe32)

*Ref 6: Create Virtual Machine*

7) Start by selecting the Resource Group we just created in the drop-down menu and then give your VM a name. As for your region just like before make sure it's set to the closest one. Change the Security type to "Standard" and the Image to "Ubuntu Server 24.04 LTS".

![1](https://github.com/user-attachments/assets/f29c4ecd-7825-41c4-99e3-5af7dd3db848)

*Ref 6: Virtual Machine Details Part 1*

8) Next on Size select Standard_B1 or 1vcpu and 1 GiB of memory. You may have to change availability zones depending on which one you select. For Authentication, we are going to select Password and then create a username and password. Then select "Next: Disks" at the bottom.

![1](https://github.com/user-attachments/assets/83228e1e-ee76-42ff-a045-e2eed1d0152f)

*Ref 7: Virtual Machine Details Part 2*

9) In the Disks section we will leave it as it is, click Networking at the bottom to continue. Whenever you create a virtual machine a Virtual Network and Network Security Group will be created alongside it so leave everything in this section the as it is. Click Review + create and then once it is done validating click Create in the bottom left corner.

![1](https://github.com/user-attachments/assets/114b9ce4-2b74-4172-921d-da92df6a0a95)
![2](https://github.com/user-attachments/assets/14d9882e-49af-4469-a9c3-a2684e1683f1)
![3](https://github.com/user-attachments/assets/41f39dcb-5d72-466e-a877-1095b7af4950)

*Ref 8: Virtual Machine Created*

10) Click on Home in the top left corner and you should see your Linux Honeypot VM under Resources. Select your VM and you should your public IP address towards the right of the screen. By default, your Network Security Group aka Firewall is allowing any IP to connect to your new VM from the Internet. Until we get everything set up let's change this so our local computer is the only thing able to connect to our new VM for security purposes. To do that let's navigate to our Network Security Groups by finding it in our search bar then select our NSG. Under settings select Inbound security rules then the SSH security rule to edit the settings. Change the Source to "My IP address" and click save.

![1](https://github.com/user-attachments/assets/e7c87d3d-8c35-4655-b781-1967dd3c8654)
![2](https://github.com/user-attachments/assets/fd52fdaf-8fd3-4763-a163-752437bc9a20)

*Ref 9: NSG*

11) Now we will use Powershell to SSH into our Linux VM, so navigate over to VM under Virtual Machines to get your public IP address.

![1](https://github.com/user-attachments/assets/727685ce-8ed9-4a03-b76b-d2cae4e75385)

*Ref 10: Lunix VM Public IP*

12) Now open up Powershell on your local computer and type in ssh followed by the username you created, followed by a @ sign, followed by the public IP of your Linux VM. Type yes, followed by your password and you should be logged in now.

![2](https://github.com/user-attachments/assets/60906914-1417-406e-abca-168342232e0b)

*Ref 11: SSH Login*

13) Next we will update and upgrade our repositories on our Linux VM with the following command:
```
sudo apt-get update && sudo apt-get upgrade -y
```
14) The next command will be to install all the dependencies to install Cowrie
```
sudo apt-get install git python3-virtualenv libssl-dev libffi-dev build-essential libpython3-dev python3-minimal authbind virtualenv python3-venv
```

15) Next add a user named Cowrie with the following command and hit Enter to leave all the next info default then type Y to continue.
```
sudo adduser --disabled-password cowrie
```

![1](https://github.com/user-attachments/assets/120878c0-c24b-489b-9bfa-c020966294a2)

*Ref 12: Add Cowrie User*

16) Change into our new Cowrie user.
```
sudo su cowrie
```
17) Change into our home directory.
```
cd /home/cowrie
```
18) Clone Cowrie's github.
```
git clone http://github.com/cowrie/cowrie
```
19) This command should create a new directory named cowrie in the current directory we are in. Now lets go ahead and change into that.
```
cd cowrie
```
20) Now we want to setup our virtual environment with Python.
```
python3 -m venv cowrie-env
```
```
source cowrie-env/bin/activate
```

![1](https://github.com/user-attachments/assets/78ae23ca-c5fc-48ac-86c9-8a43b9f4635d)

*Ref 13: Cowrie Virtual Environment*

21) Now we need to install and upgrade pip which is a package manager for Python, along with all the requirements.

```
python3 -m pip install --upgrade pip
```
```
python3 -m pip install --upgrade -r requirements.txt
```
22) Next we will create a new configuration file for Cowrie to enable Telnet which is an insecure protocol that will make it easier for attackers. To do this first change into the /etc directory and open the newly created cowrie.cfg file into nano. Once open in nano copy the file information from the screenshot below to enable telnet and then hold ctrl + X then Y to save.

```
cd /etc
```
```
nano cowrie.cfg
```
![1](https://github.com/user-attachments/assets/48861320-b5ba-456d-86dd-ea43b58e5ab6)

*Ref 14: Telnet*

23) The last thing to do here is start Cowrie, so we will need to go back one directory and into the bin directory. Inside this directory is a file named Cowrie, go ahead and run it.

```
cd ..
```
```
cd /bin
```
```
./cowrie start
```

![1](https://github.com/user-attachments/assets/3c80a807-68a5-405b-8456-bca0fa0d75ae)

*Ref 15: Start Cowrie*

24) With Cowrie now up and running there are a few things you should know... By default, Cowrie listens on port 2222 for any incoming SSH connections. If you remember the SSH firewall rule from earlier it was set to only allow incoming connections over port 22. Let's head back into our Network Security Group -> Incoming security rules -> select Custom under Service and add port 2222. 

![1](https://github.com/user-attachments/assets/c569534c-7ac3-4efc-ac37-0350acb94bc3)

*Ref 16: SSH Port 2222*

25) Also, there are two log files that you should know about as well located in /home/cowrie/cowrie/var/log/cowrie named cowrie.json and cowrie.log. Inside this log file is going to contain all the commands the attackers run once they log in to our machine. To generate some log data open up a new Powershell window and complete some failed login attempts through SSH. Now that we have this ready to go we want to save this JSON file on our host machine. Open up a new Powershell window as Administrator and SSH back into our Linux machine user with the actual username we created. Next, navigate to the path of our JSON file and run the following command to create a Python server hosting the files in our current directory.

![1](https://github.com/user-attachments/assets/89ffee6f-6699-47c7-9216-64962826bd27)

*Ref 17: Failed Logins*

```
cd /home/cowrie/cowrie/var/log/cowrie
```
```
python3 -m http.server 9999
```

26) If we try and connect to this Python server now we wouldn't be able to because of our firewall rule only allowing ports 22 and 2222. Let's head back over to our Network Security Group like before and add our new port of 9999. After that is complete type in the IP address of our Linux VM followed by a colon and then the port number to connect. From here open the cowrie.log file we created, right-click to save as and put it in our Downloads folder.

![1](https://github.com/user-attachments/assets/bffcb849-d9f9-4cdb-a9a7-f09fd6f906b5)

*Ref 18: Python Server Port 9999*

![1](https://github.com/user-attachments/assets/92be94ca-485d-4fc2-a377-09ea06395d13)

*Ref 19: Cowrie.Log*

27) Now we are done with Cowrie! Next in Part 2 of this project we will finish setting things up in Microsoft Azure!
