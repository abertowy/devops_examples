# AZ-104 Prerequisites: Manage services with Azure Portal

## Table of contents
1. [Azure management options](#question1)
2. [Azure Cloud Shell](#question2)
3. [Bash](#question3)
4. [PowerShell](#question4)
5. [Azure Resource Manager (ARM) template](#question5)
6. [ARM template file structure](#question6)
7. [Deploy an ARM template to Azure](#question7)
8. [Parameters and outputs in ARM templates](#question8)

## 1. Azure management options <a name="question1"></a>

Tools:
- **Azure portal** for interacting with Azure via a Graphical User Interface (GUI)  
    The Azure portal is a public website you can access with any web browser. Once you sign in with your Azure account, you can create, manage, and monitor Azure services and resources.  
    The Azure portal is often the best interface for carrying out single tasks, or when you want to look at configuration options in detail.  
    Generally speaking, the portal doesn't let you automate repetitive tasks.  
- **Azure PowerShell** and **Azure Command-Line Interface (CLI)** for command-line and automation-based interactions with Azure  
    Azure PowerShell lets you connect to your Azure subscription and manage resources.  
    Azure CLI is a command-line program that connects to Azure and executes administrative commands on Azure resources. Azure CLI can run on Windows, Linux, or macOS.  
    Can be used for repetetive tasks  
- **Azure Cloud Shell** for a web-based command-line interface  
    Azure Cloud Shell is an interactive, authenticated, browser-accessible shell for managing Azure resources using scripting tools like Azure CLI or Azure PowerShell. The Cloud Shell also has many other developer tools available, such as text editors, source-control tools, databases, and more.  
- **Azure mobile app** for monitoring and managing your resources from your mobile device  
    allows you to access, manage, and monitor all your Azure accounts and resources from your iOS or Android phone or tablet.  
    - Check the current status and critical metrics of your services.
    - Stay informed with notifications and alerts about important health issues.
    - Review the latest Azure alerts.
    - Start, stop, and restart virtual machines or web apps.
    - Connect to your virtual machines.
    - Manage permissions with role-based access control (RBAC).
    - Use the Azure Cloud Shell to run saved scripts or perform administrative tasks.

## 2. Azure Cloud Shell <a name="question2"></a>

**Azure Cloud Shell** (https://shell.azure.com/) is a command-line environment you can access through your web browser. You can use this environment to manage Azure resources, including VMs, storage, and networking.  
  
Azure Cloud Shell also provides cloud storage to persist files such as SSH keys, scripts, and more. This functionality lets you access important files in between sessions and with different machines. Finally, you can use the Cloud Shell editor to make changes to files, such as scripts, that are saved into this cloud storage directly from the Cloud Shell interface.  
  
When using Cloud Shell, you might also need to run scripts or use files for different actions. You can persist files on Cloud Shell by using the Azure CloudDrive: upload, download, manage file share.  
  
### You can use Azure Cloud Shell to:
- Open a secure command-line session from any browser-based device.
- Interact with Azure resources without the need to install plug-ins or add-ons to your device.
- Persist files between sessions for later use.
- Use either Bash or PowerShell, whichever you prefer, to manage Azure resources.
- Edit files (such as scripts) via the Cloud Shell editor.

### You shouldn't use Azure Cloud Shell if:
- You intend to leave a session open for more than 20 minutes for long running scripts or activities. In these cases, your session is disconnected without warning, and the current state is lost.
- You need admin permissions, such as sudo access, from within the Azure CLI or PowerShell environment.
- You need to install tools that aren't supported in the limited Cloud Shell environment, but instead require an environment such as a custom virtual machine or container.
- You need storage from different regions. You might need to back up and synchronize this content since only one region can have the storage allocated to Azure Cloud Shell.
- You need to open multiple sessions at the same time. Azure Cloud Shell allows only one instance at time and isn't suitable for concurrent work across multiple subscriptions or tenants.

## 3. Bash <a name="question3"></a>

**Bash** is a vital tool for managing Linux machines. The name is short for "Bourne Again Shell."  
A **shell** is a program that commands the operating system to perform actions. You can enter commands in a console on your computer and run the commands directly, or you can use scripts to run batches of commands.  
As Peter Salus summarized in his book A Quarter Century of Unix, three of the "big ideas" embodied in Unix are:  
- Programs do one thing and do it well
- Programs work together
- Programs use text streams as the universal interface

`command [options] [arguments]`  
  
**Wildacrds:**
- `*`: asterisk, represents zero characters or a sequence of characters
- `?`: question mark, represents a single character
- `[]`: square brackets, denote groups of characters. Example: `ls *.[jp]* -> .jpg, .jpeg`
- `case-sensitive`: `ls *.[jpJP]*`
- `range`: `ls [a-z]* -> showsall files starts from the lower-case letter', `ls [a-zA-Z]* -> from any letter`
- `[0-9]`: numeric range
  
`w` command: displays information about the users currently on the computer system and those users' activities. `w` shows user names, their IP addresses, when they logged in, what processes they're currently running, and how much time those processes are consuming.  

**Bash I/O operators:**
- `<` for redirecting input to a source other than the keyboard
- `>` for redirecting output to destination other than the screen
- `>>` for doing the same, but appending rather than overwriting
- `|` for piping output from one command to the input of another

## 4. PowerShell <a name="question4"></a>

PowerShell consists of two parts: a command-line shell and a scripting language.
  
### Features
1. **Traditional shell**:
    - **Built-in help system**: help system in PowerShell provides information about commands and also integrates with online help articles.
    - **Pipeline**: Traditional shells use a pipeline to run many commands sequentially. The output of one command is the input for the next command.
    - **Aliases**: Aliases are alternate names that can be used to run commands. PowerShell supports the use of common aliases such as cls (clear the screen) and ls (list the files).
2. **Differs from traditional shell**:
    - It operates on **objects over text**. In a command-line shell, you have to run scripts whose output and input might differ, so you end up spending time formatting the output and extracting the data you need. By contrast, in PowerShell you use objects as input and output. That means you spend less time formatting and extracting.
    - It has **cmdlets**. Commands in PowerShell are called cmdlets (pronounced commandlets). In PowerShell, `cmdlets` are built on a common runtime rather than separate executables as they are in many other shell environments. This characteristic provides a consistent experience in parameter parsing and pipeline behavior. `Cmdlets` typically take object input and return objects. The core `cmdlets` in PowerShell are built in `.NET Core`, and are open source. You can extend PowerShell by using more `cmdlets`, scripts, and functions from the community and other sources, or you can build your own `cmdlets` in `.NET Core` or PowerShell.
  
**Cmdlets**:
- `Get-Command`: lists all of the available cmdlets on your system. Filter the list to quickly find the command you need.
- `Get-Help`: invokes a built-in help system. You can also run an alias help command to invoke `Get-Help` but improve the reading experience by paginating the response.
- `Get-Member`: the response is an object that contains many properties. Run the `Get-Member` core `cmdlet` to drill down into that response and learn more about it.
  
**Flags**:
- `-Noun`: targets the part of the command name that's related to the noun. Example: `Get-Command -Noun alias*`
- `-Verb`: targets the part of the command name that's related to the verb. Example: `Get-Command -Verb Get -Noun alias*`

## 5. Azure Resource Manager (ARM) template <a name="question5"></a>

**Advantages** to `infrastructure as code` are:
- Consistent configurations
- Improved scalability
- Faster deployments
- Better traceability

**ARM templates** are `JavaScript Object Notation` (`JSON`) files that define the infrastructure and configuration for your deployment. The template uses a **declarative** syntax. The **declarative** syntax is a way of building the structure and elements that outline what resources look like without describing the control flow. **Declarative** syntax is different than **imperative** syntax, which uses **commands** for the computer to perform. Imperative scripting focuses on specifying each step in deploying the resources.  
  
ARM templates allow you to declare what you intend to deploy without having to write the sequence of programming commands to create it. In an ARM template, you specify the resources and the properties for those resources. Azure Resource Manager then uses that information to deploy the resources in an organized and consistent manner.  
  
**Benefits** of using `ARM templates`:
- `ARM templates` allow you to automate deployments and use the practice of infrastructure as code (`IaC`)
- `ARM templates` are **idempotent**, which means you can deploy the same template many times and get the same resource types in the same state
- ARM template deployments finish faster than scripted deployments, because Resource Manager orchestrates deploying the resources so they're created in the correct order. When possible, resources are created in parallel
- Resource Manager also has built-in validation
- you can break your `ARM templates` into smaller, **reusable** components. You can link these smaller templates together at deployment time. You can also **nest** templates inside other templates
- You can also integrate your `ARM templates` into `CI/CD` tools like `Azure Pipelines`, which can **automate** your release pipelines for **fast and reliable** application and infrastructure updates. By using `Azure DevOps` and `ARM template` tasks, you can continuously build and deploy your projects.

## 6. ARM template file structure <a name="question6"></a>

1. `schema`: A **required** section that defines the **location of the JSON schema** file that describes the structure of JSON data. The version number you use depends on the scope of the deployment and your JSON editor.
2. `contentVersion`: A **required** section that defines the **version of your template** (such as 1.0.0.0). You can use this value to document significant changes in your template to ensure you're deploying the right template.
3. `apiProfile`: An **optional** section that defines a **collection of API versions for resource types**. You can use this value to avoid having to specify API versions for each resource in the template.
4. `parameters`: An **optional** section where you define **values that are provided during deployment**. You can provide these values in a parameter file, by command-line parameters, or in the Azure portal.
5. `variables`: An **optional** section where you define **values that are used to simplify template language expressions**.
6. `functions`: An **optional** section where you can define **user-defined functions** that are available within the template. User-defined functions can simplify your template when complicated expressions are used repeatedly in your template.
7. `resources`: A **required** section that defines the **actual items you want to deploy or update** in a resource group or a subscription.
8. `output`: An **optional** section where you specify the **values that are returned** at the end of the deployment.

## 7. Deploy an ARM template to Azure <a name="question7"></a>

- Deploy a local template
- Deploy a linked template
- Deploy in a continuous deployment pipeline

```bash
az login
az account list-locations
az group create --name {name of your resource group} --location "{location}"
templateFile="{provide-the-path-to-the-template-file}"
az deployment group create --name blanktemplate --resource-group myResourceGroup --template-file $templateFile
```
  
Use linked templates to deploy complex solutions. You can break a template into many templates and deploy these templates through a main template. When you deploy the main template, it triggers the linked template's deployment. You can store and secure the linked template by using a SAS token.  
A CI/CD pipeline automates the creation and deployment of development projects, which includes ARM template projects. The two most common pipelines used for template deployment are Azure Pipelines or GitHub Actions.  

Example: `Microsoft.Storage/storageAccounts`  
```JSON
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.1",
  "apiProfile": "",
  "parameters": {},
  "variables": {},
  "functions": [],
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2023-05-01",
      "name": "learntemplatestorage123",
      "location": "westus",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "StorageV2",
      "properties": {
        "supportsHttpsTrafficOnly": true
      }
    }
  ],
  "outputs": {}
}
```

## 8. Parameters and outputs in ARM templates <a name="question8"></a>

ARM-template parameters let you customize the deployment by providing values that are tailored for a particular environment.  
The available properties for a parameter are:  
```JSON
"parameters": {
  "<parameter-name>": {
    "type": "<type-of-parameter-value>",
    "defaultValue": "<default-value-of-parameter>",
    "allowedValues": [
      "<array-of-allowed-values>"
    ],
    "minValue": <minimum-value-for-int>,
    "maxValue": <maximum-value-for-int>,
    "minLength": <minimum-length-for-string-or-array>,
    "maxLength": <maximum-length-for-string-or-array-parameters>,
    "metadata": {
      "description": "<description-of-the-parameter>"
    }
  }
}

"outputs": {
  "<output-name>": {
    "condition": "<boolean-value-whether-to-output-value>",
    "type": "<type-of-output-value>",
    "value": "<output-value-expression>",
    "copy": {
      "count": <number-of-iterations>,
      "input": <values-for-the-variable>
    }
  }
}
```
The allowed types of parameters are:
- `string`
- `secureString`
- `integers`
- `boolean`
- `object`
- `secureObject`
- `array`
  
Use **parameters** for settings that **vary** according to the environment; for example, **SKU, size, or capacity**. Also use parameters for resource names that you want to specify yourself for easy identification or to comply with internal naming conventions. Provide a description for each parameter, and use **default values** whenever possible.  
  
For security reasons, never hardcode or provide default values for usernames and/or passwords in templates. Always use **parameters for usernames and passwords** (or secrets). Use `secureString` for all **passwords and secrets**. If you pass sensitive data in a JSON object, use the `secureObject` type. Template parameters with `secureString` or `secureObject` types can't be read or harvested after the deployment of the resource.  
  
```JSON
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.1",
  "apiProfile": "",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {},
  "functions": [],
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2023-05-01",
      "name": "learntemplatestorage123",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('storageAccountType')]"
      },
      "kind": "StorageV2",
      "properties": {
        "supportsHttpsTrafficOnly": true
      }
    }
  ]
  "outputs": {
    "storageEndpoint": {
      "type": "object",
      "value": "[reference('learntemplatestorage123').primaryEndpoints]"
    }
  }
}
```
```bash
templateFile="azuredeploy.json"
az deployment group create --name testdeployment1 --template-file $templateFile --parameters storageAccountType=Standard_LRS
```
