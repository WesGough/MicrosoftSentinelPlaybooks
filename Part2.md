# Microsoft Sentinel Playbooks Part 2

## Objective 

### Skills Learned

### Tools Used

### Step-By-Step Guide

1) Now that we have a VM with Cowrie running and the JSON log file on our host machine, we want to start creating a Log Analytic Workspace in Azure so we can start querying our data. Navigate to the Log Analytics Workspace by typing it in your search bar and click Create Log Analytics workspace.

![1](https://github.com/user-attachments/assets/1eb5ac53-d7b7-4646-a484-1bb99ac264e5)

*Ref 1: Log Analytics Workspace*

2) Find the Resource group we created in the drop-down menu and select it, then give your Log Analytics workspace and name then click Review + Create in the bottom left corner of the screen. Once validation passes click Create.

![1](https://github.com/user-attachments/assets/83303e0b-1400-4fd8-a961-49a1b2d5fc51)

*Ref 2: Creation*

3) Once your deployment is complete, click on Go to resource. In order for us to search for the JSON log file we created earlier we must create a table to store that log file. Which you can do by clicking Tables under settings then New custom log (MMA-based).
        
![1](https://github.com/user-attachments/assets/240d8741-182e-4440-8752-ba2fc404e9b2)
![2](https://github.com/user-attachments/assets/5f106223-8866-44c8-872a-1a577141fdf2)

*Ref 3: Create Table*

4) Upload your JSON log file we saved in our Downloads folder and click Next. You should see the JSON log file we created in the Preview window... go ahead and hit Next again.

![1](https://github.com/user-attachments/assets/cecab8b4-3e58-4dcc-b9fe-d52845f63d99)

*Ref 4: Create Table cont*
