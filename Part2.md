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

3) Once your deployment is complete, click on Go to resource. For us to search for the JSON log file we created earlier we must create a table to store that log file. Which you can do by clicking Tables under settings then New custom log (MMA-based).
        
![1](https://github.com/user-attachments/assets/240d8741-182e-4440-8752-ba2fc404e9b2)
![2](https://github.com/user-attachments/assets/5f106223-8866-44c8-872a-1a577141fdf2)
*Ref 3: Create Table*

4) Upload your JSON log file we saved in our Downloads folder and click Next. You should see the JSON log file we created in the Preview window... go ahead and hit Next again.

![1](https://github.com/user-attachments/assets/cecab8b4-3e58-4dcc-b9fe-d52845f63d99)
*Ref 4: Create Table cont*

5) In the drop-down menu under Type select Linux.

- Type in the file path where our log is stored then hit Next
   
![Screenshot 2025-01-05 165056](https://github.com/user-attachments/assets/0d2f0bca-ce7f-4853-810c-7b4fbebed7a6) 
*Ref 5: File Path*

- Type in Custom log name and hit Next and Create

![image](https://github.com/user-attachments/assets/d5ccb87e-6f5f-464d-a5d5-b76ea5d2dc26)
*Ref 5: Custom Log Name*

6) Refresh the page then click on the 3 dot of the table we just created.
- Select Edit Schema

![image](https://github.com/user-attachments/assets/f3e95641-ae28-4a8b-9669-f4a0b10ff521)
*Ref 6: Edit Schema*

- Select Migrate to manual schema management and then hit Ok

![image](https://github.com/user-attachments/assets/6e6b0270-8805-4b43-9b62-e82da351dc7f)
*Ref 7: Schema management*

7) Next we will need to create a Data Collection Endpoint by searching for this in the search bar.
- Select Create data collection endpoint
- Give the Endpoint a name and select the Resource group we created then select Review + Create
- Select Create one more time

![image](https://github.com/user-attachments/assets/9e086ef3-a0c7-4d50-aaea-76aa79b19aaa)
*Ref 8: Collection Enpoint*

8) Now that we have the endpoint created, the next thing to do is create a Data collection rule to specify exactly what we want to collect from our endpoint. Navigate to Data collection rules by searching for it in the search bar.
- Select Create data collection rule
- Give the rule a name
- Select the Resource Group we created
- Select the appropriate Region and Platform Type
- Finally, select our Data Collection Endpoint and then select Next: Resources

![image](https://github.com/user-attachments/assets/7a916aa9-bd3a-4a9d-b85c-12426dfd95b6)
*Ref 9: Data Collection Rule*

- Select Add Resources
- 
![image](https://github.com/user-attachments/assets/aa4234ed-37ad-4850-b1e5-a1437a150a2e)
*Ref 10: Resources*

- Select our Resource Group and then click Apply

![image](https://github.com/user-attachments/assets/4d4aa025-ede8-434e-85c6-5133b1e8bd86)
*Ref 11: Resource Group*

- Select Enable Data Collection Endpoints box
- Select LinuxMachine in the drop-down under Data collection endpoint
- Then click on Next: Collect and deliver

![image](https://github.com/user-attachments/assets/f18044f0-ce14-4633-8eaa-73664eeafa8c)

*Ref 12: Checkbox*

- Select Add data source

suod![image](https://github.com/user-attachments/assets/2e4b6892-4f11-4545-8b44-96b55bf663de)

- Under Data source type pick Custom JSON Logs

