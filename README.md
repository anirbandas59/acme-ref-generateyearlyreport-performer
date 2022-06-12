# ACME_REF_GenerateYearlyReport_PerformerBot

Robotic Enterprise Framework performer bot to get work items from Orchestrator queue and generate yearly report and update the work item subsequently

### Documentation is included in the Documentation folder

[REFrameWork Documentation](https://github.com/UiPath/ReFrameWork/blob/master/Documentation/REFramework%20documentation.pdf)

### REFrameWork Template

**Robotic Enterprise Framework**

- Built on top of _Transactional Business Process_ template
- Uses _State Machine_ layout for the phases of automation project
- Offers high level logging, exception handling and recovery
- Keeps external settings in _Config.xlsx_ file and Orchestrator assets
- Pulls credentials from Orchestrator assets and _Windows Credential Manager_
- Gets transaction data from Orchestrator queue and updates back status
- Takes screenshots in case of system exceptions

### How It Works

1. **INITIALIZE PROCESS**

- ./Framework/_InitiAllSettings_ - Load configuration data from Config.xlsx file and from assets
- ./Framework/_GetAppCredential_ - Retrieve credentials from Orchestrator assets or local Windows Credential Manager
- ./Framework/_InitiAllApplications_ - Open and login to applications used throughout the process

2. **GET TRANSACTION DATA**

- ./Framework/_GetTransactionData_ - Fetches transactions from an Orchestrator queue defined by Config("OrchestratorQueueName") or any other configured data source

3. **PROCESS TRANSACTION**

- _Process_ - Process trasaction and invoke other workflows related to the process being automated
- ./Framework/_SetTransactionStatus_ - Updates the status of the processed transaction (Orchestrator transactions by default): Success, Business Rule Exception or System Exception

4. **END PROCESS**

- ./Framework/_CloseAllApplications_ - Logs out and closes applications used throughout the process

### For New Project

1. Check the Config.xlsx file and add/customize any required fields and values
2. Implement InitiAllApplications.xaml and CloseAllApplicatoins.xaml workflows, linking them in the Config.xlsx fields
3. Implement GetTransactionData.xaml and SetTransactionStatus.xaml according to the transaction type being used (Orchestrator queues by default)
4. Implement Process.xaml workflow and invoke other workflows related to the process being automated
