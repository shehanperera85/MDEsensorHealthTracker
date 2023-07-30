Power of Advanced Hunting + Automation = Success
My approach uses KQL to run a hunting query to identify the devices with an inactive or misconfigured sensor health state and notify via Teams every 24 hours. This query will return the latest record for the device that has the Sensor health state.

Note: LastUpdatedTime in my query or Last Device Update in the Device inventory is the Time and date of the last received full device report. A device typically sends a full report every 24 hours.

In this way, for the notification time gap, I think 24hrs is a good interval.

Workflow in a nutshell 👇🏽


Prerequisites
Least privileges of View data- security operations role is required for Viewing hunting data.
![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/5904ecac-b93e-48b2-8e40-f2f6c78f6d11)


Create your Hunting Query
DeviceInfo

Create the Logic App
For this part, you need to have an Azure subscription.  

Create a resource > Logic App (by providing the name and other attributes)
Next Steps
Go to the Workflows section
![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/9a284837-eacf-44cb-a7be-77c60aa58034)

Add a new Workflow with the type Stateful
![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/41f0c4dc-a3db-4ef2-8781-af0f411b376e)

Add the trigger

![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/1883937c-afef-4791-9042-d90aa5886c8a)

Add an Initialize Variable action
![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/4b8a4edd-a37c-404a-87f6-0d9830280e46)

Create the Action by adding Advanced Hunting under Microsoft Defender ATP and Sign-in with the account
![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/6dfb19a7-da35-4cac-8fd4-6d2a0a7a3fc0)

Add your query
![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/12d7824c-eb13-43e8-8fe6-3c3631e73ecd)

Add a Set Variable action so the Value “Results” can be added to the array
![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/ad1c0979-b03d-448e-b80f-62a25c7b075b)

Add a Create HTML table from the “KQL-Results” array so it will be cleaned for presentation
![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/dd967a30-e2f1-40d6-b033-928e6b379137)

And finally, add the Teams connection to post the results as a message. As you can see, I have included the Troubleshooting guide in the message.
![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/bc6e75ce-e4b3-4711-a7eb-89a45f130ec5)

The result will be something similar to this. The Sensor state for the devices shows Active. When I was writing this blog, I didn’t have an inactive device so I slightly changed my query to show the Active devices. But the result will be similar to this output, but with Inactive or Misconfigured sensor state.
![image](https://github.com/shehanperera85/MDEsensorHealthTracker/assets/98259062/09493a88-609b-4ffa-9e1a-75a7356c57a4)
