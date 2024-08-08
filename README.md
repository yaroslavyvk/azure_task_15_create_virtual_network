# Create Virtual Network

I'm sure you missed working on your TODO app startup! I have some good news for you: after some negotiations you finally got invesments! Now, when your startup is at scaling phase, you are getting concerned about security and scalability. To address those concerns, you decided to build a private network for your infrastructure. 

In this task you will plan and deploy a virtual network for the TODO web app. 

## How to Complete Tasks in This Module 

Tasks in this module are relying on 2 PowerShell scripts: 

- `scripts/generate-artifacts.ps1` generates the task "artifacts" and uploads them to cloud storage. An "artifact" is evidence of a task completed by you. Each task will have its own script, which will gather the required artifacts. The script also adds a link to the generated artifact in the `artifacts.json` file in this repository — make sure to commit changes to this file after you run the script. 
- `scripts/validate-artifacts.ps1` validates the artifacts generated by the first script. It loads information about the task artifacts from the `artifacts.json` file.

Here is how to complete tasks in this module:

1. Clone task repository

2. Make sure you completed steps, described in the Prerequisites section

3. Complete the task, described in the Requirements section 

4. Run `scripts/generate-artifacts.ps1` to generate task artifacts. Script will update the file `artifacts.json` in this repo. 

5. Run `scripts/validate-artifacts.ps1` to test yourself. If tests are failing - follow the recomendation from the test script error message to fix or re-deploy your infrastructure. When you will be ready to test yourself again - **re-generate the artifacts** (step 4) and re-run tests again. 

6. When all tests will pass - commit your changes and submit the solution for a review. 

Pro tip: if you stuck with any of the implementation steps - run `scripts/generate-artifacts.ps1` and `scripts/validate-artifacts.ps1`. The validation script might give you a hint on what you should do.  

## Prerequisites

Before completing any task in the module, make sure that you followed all the steps described in the **Environment Setup** topic, in particular: 

1. Ensure you have an [Azure](https://azure.microsoft.com/en-us/free/) account and subscription.

2. Create a resource group called *"mate-resources"* in the Azure subscription.

3. In the *"mate-resources"* resource group, create a storage account (any name) and a *"task-artifacts"* container.

4. Install [PowerShell 7](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7.4) on your computer. All tasks in this module use Powershell 7. To run it in the terminal, execute the following command: 
    ```
    pwsh
    ```

5. Install [Azure module for PowerShell 7](https://learn.microsoft.com/en-us/powershell/azure/install-azure-powershell?view=azps-11.3.0): 
    ```
    Install-Module -Name Az -Repository PSGallery -Force
    ```
If you are a Windows user, before running this command, please also run the following: 
    ```
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```

6. Log in to your Azure account using PowerShell:
    ```
    Connect-AzAccount -TenantId <your Microsoft Entra ID tenant id>
    ```

## Requirements

In this task, you will need to plan and deploy Azure Virtual Network. 

The virtual network should satisfy the following requirements: 
- Virtual Network address space (ip address range): 10.20.30.0/24
- Virtual Network should have 3 subnets: 
    - `webservers`
    - `database`
    - `management`
- Each subnet should fit up to 50 virtual machines

To complete the task, you need to perform the following steps: 

1. Calculate IP address ranges for your subnets. You can do it either following the approach, described in the learning matterials, or using the [online tool](https://www.davidc.net/sites/default/subnets/subnets.html). 

2. Update the Powershell script `task.ps1` to add deployment of the Virtual Network and subnets using Powershell module for Azure: 

    - Virtual Network resource should be deployed to the resource group `mate-azure-task-15`, it should be called `todoapp`. Normally, we would recommend defining a naming convention, and call it like `dev-todoapp-uksouth-vnet`, but just for the validation purposes it is easier for us to go with `todoapp`. 

    - To learn how to deploy Virtual Network and subnets, check the documentation of [New-AzVirtualNetwork](https://learn.microsoft.com/en-us/powershell/module/az.network/new-azvirtualnetwork?view=azps-12.1.0#example-3-create-a-virtual-network-with-a-subnet-referencing-a-network-security-group) (For now, skip the security group parameters - they are not mandatory)

3. Run the updated `task.ps1` script to create a cloud infrastructure for the web app. 

4. Run artifacts generation script `scripts/generate-artifacts.ps1`.

5. Test yourself using the script `scripts/validate-artifacts.ps1`.

6. Make sure that changes to both `task.ps1` and `result.json` are commited to the repo, and sumbit the solution for a review. 

7. You can keep the resources if you want to - anyway, virtual network resource itself is [free](https://azure.microsoft.com/en-us/pricing/details/virtual-network/)
