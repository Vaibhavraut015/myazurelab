Deploy Resources Using an ARM Template in the Azure Portal
Introduction
Azure Resource Manager (ARM) templates provide a powerful way to define Azure resources and configuration, by essentially using a text file. This helps with consistency and automation of resource deployments. In this hands-on lab, you will learn how to create a storage account using an ARM template and walk through modifying the template to see how parameters and variables work.

Solution
Log in to the Azure portal using the credentials provided for the lab.

Load the ARM Template Using the Azure Portal
Download the ARM template to your computer or copy the template text from the GitHub repository here.

In the Azure portal, click Create a resource.

In the Search bar, type in "template" and select the Template deployment (deploy using custom templates) option from the contextual menu.

Click Create.

On the Custom deployment page, click Build your own template in the editor.

On the Edit template page, either paste the template text you copied or click Load file and select the labstoragetemplate.json file you downloaded in the first step.

Modify the ARM Template Parameters and Variables
Add a Storage Account Kind Parameter and Modify the Existing Resource Definition to Use It
In the parameters section of the template, copy the location parameter and paste the copied text directly below it.

Change the location parameter to storageAccountKind.

Set the defaultValue to StorageV2.

In the resources section of the template, copy the [parameters('location')] value from the location property, and paste it as the value for the kind property below.

For the kind property, change the value to [parameters('storageAccountKind')].

Create a Variable to Provide a Unique Storage Account Name Using the Storage Account Name Parameter and a Unique String Function
Above the resources section, add a new section called variables.

Add a new variable named uniqueStorageAccountName.

Give the uniqueStorageAccountName variable a value of [concat(parameters('storageAccountName'),uniqueString(resourceGroup().id))], which combines the storageAccountName parameter and a string of 13 characters that are unique to the resource group.

In the resources section, change the value for the name property to variables('uniqueStorageAccountName').

Note: Make sure to add a trailing comma to the end of your variables configuration, after the closed curly brace, to make it usable.

Hard-Code in the Location for the Storage Account Resource
In the resources section, change the value for the location property to West US.

In the parameters section, delete the code for the location parameter:

"location": {
  "type": "string",
  "defaultValue": "[resourceGroup().location]"
},
Click Save to save the changes to the template.

Deploy the ARM Template Using the Parameters File
On the Custom deployment page, click Edit parameters.

In the parameters file, set the value for storageAccountName parameter to azurelab.

Leave the value for the storageAccountKind parameter as StorageV2.

Click Save.

Verify that the values you just set in the parameters file now appear in the Storage Account Name and Storage Account Kind fields under Parameters.

Leave the Subscription field as the default selection, which is the existing subscription provided for the lab.

From the Resource group drop-down, select the existing resource group provided for the lab.

Note that, once you select the provided subscription and resource group, the Region updates to West US and cannot be modified.

Click Review + create.

When validation has passed, click Create.

Once deployment is complete click Go to resource.

Note the following, which were set in the template and the parameters file:

The name of the storage account, which should be azurelab appended with a unique string of characters.
The Location is West US.
The Account kind is StorageV2.
Conclusion
Congratulations — you've completed this hands-on lab!
