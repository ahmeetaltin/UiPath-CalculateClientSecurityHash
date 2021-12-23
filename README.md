This is the 'Calculate Client Security Hash' process which is without API documentation and the 1st project for the Advanced Certification.


https://www.youtube.com/watch?v=1_-PpuNv5Zw


Step    Short Description

1.1     Open the ACME System 1 Web Application.
 
1.2     Log in to System 1. Required input data: email and password. 

1.3     Access the Dashboard - the central location, where the user can pick a specific menu item.

1.4     Access the Work Items listing to view all the available tasks to be performed (Output data: Work Items).

1.5     For each activity of the WI5 type, perform the following steps: 

1.5.A   Open the Details page of the selected activity to retrieve the Client Details. 

1.5.B   Open the SHA1 Online webpage - http://www.sha1-online.com, and provide the following input: - ClientID ClientCountry. Replace all the variables with the corresponding values. Use dashes between each item and the above. 

1.5.C   Retrieve the Client Security Hash value from the webpage. 

1.5.D   Go back to Work Item Details and open Update Work Item. 

1.5.E   Set the status to “Completed”. Add a comment with the obtained SecurityHash.

1.6 Continue with the next WI5 Activity. 



### Documentation is included in the Documentation folder ###

[REFrameWork Documentation](https://github.com/UiPath/ReFrameWork/blob/master/Documentation/REFramework%20documentation.pdf)

### REFrameWork Template ###
**Robotic Enterprise Framework**

* Built on top of *Transactional Business Process* template
* Uses *State Machine* layout for the phases of automation project
* Offers high level logging, exception handling and recovery
* Keeps external settings in *Config.xlsx* file and Orchestrator assets
* Pulls credentials from Orchestrator assets and *Windows Credential Manager*
* Gets transaction data from Orchestrator queue and updates back status
* Takes screenshots in case of system exceptions


### How It Works ###

1. **INITIALIZE PROCESS**
 + ./Framework/*InitiAllSettings* - Load configuration data from Config.xlsx file and from assets
 + ./Framework/*GetAppCredential* - Retrieve credentials from Orchestrator assets or local Windows Credential Manager
 + ./Framework/*InitiAllApplications* - Open and login to applications used throughout the process

2. **GET TRANSACTION DATA**
 + ./Framework/*GetTransactionData* - Fetches transactions from an Orchestrator queue defined by Config("OrchestratorQueueName") or any other configured data source

3. **PROCESS TRANSACTION**
 + *Process* - Process trasaction and invoke other workflows related to the process being automated 
 + ./Framework/*SetTransactionStatus* - Updates the status of the processed transaction (Orchestrator transactions by default): Success, Business Rule Exception or System Exception

4. **END PROCESS**
 + ./Framework/*CloseAllApplications* - Logs out and closes applications used throughout the process


### For New Project ###

1. Check the Config.xlsx file and add/customize any required fields and values
2. Implement InitiAllApplications.xaml and CloseAllApplicatoins.xaml workflows, linking them in the Config.xlsx fields
3. Implement GetTransactionData.xaml and SetTransactionStatus.xaml according to the transaction type being used (Orchestrator queues by default)
4. Implement Process.xaml workflow and invoke other workflows related to the process being automated
