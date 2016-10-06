# Overview
Before we can provision a Platform Instance based on a Platform Blueprint, we need to define a Platform Model. 

The Platform Model maps the Platform Blueprint to the target environment for our Oracle Middleware platform and provides environment specific configuration details. The target environment can be on premise or on the cloud.

When we create the Platform Model, we also have the ability to override many of the configurations defined in the Platform Blueprint, this provides a mechanism to safely manage configuration differences between environments. For example, you may want for detailed logging levels in a Development or Test environment.

For each Platform Instance that we want to create, we need to create a corresponding Platform Model in MyST.

## Create Platform Model for Pre-Existing Infrastructure
From the side menu navigate to`Modeling` > `Platform Model`, this will display a list of existing Platform Models. Click on `Create New` in the top right-hand corner of the screen. This will launch the `New Platform Model` wizard.

![](img/ModelBasic.PNG)

In the initial dialogue we need to specify the following details about our Platform Model:

* **Platform Blueprint** - The Platform Blueprint that we will use for our Platform Model.
* **Platform Blueprint Version** - The version of the Platform Blueprint that we will use for our Platform Model.
* **Environment Type** - The Environment Type for the Platform Model.
* **Name** - Short hand name for the Platform Model.
* **Description** - A longer description of the Platform Model.
* **Workspaces** - This defines the Workspaces to which the Platform Model belongs. See Role Based Access Control for further details.

>> Note: MyST will set the initial version of the Platform Model to 
`<Platform Blueprint Version>-1`. See Platform Blueprint and Model Versioning for further details.

Once we have entered the basic details about our Platform Model click `Next`.

### Select Infrastructure Provider
Next, we need to specify the Infrastructure Provider for our Platform Model. From the corresponding drop-down, select a Pre-Existing Infrastructure Provider. MyST will list all the target hosts within the in the Pre-Existing Infrastructure provider for the Platform Model Environment Type.

![](/Part3/createPlatformModel/img/ModelInfrastructure.PNG)

Once done, click `Next`.

### Specify Compute Group Size
For each Compute Group defined within the Platform Blueprint we need to specify the number of nodes to use.
![](/Part3/createPlatformModel/img/ModelComputeGroup.PNG)

In addition, we can also specify whether we want to have a stand alone admin server, in which case it will be created within its own compute group. MyST will default to what is specified in the Platform Blueprint.

If in the Platform Blueprint, we specified a stand alone Admin Server, and then choose to override that, then we will also need to specify to which compute group we want to target the Admin Server.

Once done, click `Next`.

### Map to Pre-Existing Servers
Once we have specified the number of nodes for each compute group, the next step is to map each Node to a corresponding Pre-Existing Host in the specified infrastrcuture provider.

MyST will list out each node required by the Platform Model. Againts each node there will be a drop down box, which will list the target hosts available to map the node. For each node, select the target host. Only hosts available from the specified environment will be available for selection.

![](/Part3/createPlatformModel/img/ModelInfrastructureMap.PNG)

>>Note: Care should be taken not to assign multiple nodes within the same Platform Model to the same host.

Once done, click `Next`.

### Specify Platform Model Configurations
The final stage is to specify configuration properties that are specifc to the Platform Model.
![](/Part3/createPlatformModel/img/ModelConfigureGeneral.PNG)

For the Platform Model we need to specify the following details :
* **Domain Name** - This is the WebLogic Domain name, it will default to the value specified in the Platform Blueprint, but can be overridden in the Platform Model.
* **WebLogic Admin User* - Enter the WebLogic Admin user, it defauts to Weblogic.
* **Weblogic Admin Password** - Enter the password to be used for the WebLogic Admin User.
* **JDBC Data Source type** - This option is used to specify the Data Source Type for Oracle Middleware specific schemas which are created by the Oracle Middleware Repository Creation Utility (RCU). This will default to the value specified in the Platform Blueprint, but can be overridden in the Platform Model.
* **RCU Components** - This details the RCU specific schemas that will be created. This is pre-populated based on the Oracle Middlware Components specified in the Platform Blueprint, this is for information purposes only and can't be modified.
* **RCU Database URL** - Enter the database URL for the database that will host the 
* **RCU Prefix** - Specify the RCU Prefix to be used. The prefix is prepended to and separated from the schema name with an underscore (_) character.
* **RCU Database Password** Enter the password to be used for each of the schema owners created by RCU.
* **RCU SYS User** - Enter the user name for the RCU database. This should be a username with DBA or SYSDBA priviliges, for example SYS.
* **RCU SYS Password** - Enter the password for the RCU Sys User.

>> Note: All passwords stored by MyST are encrypted. 


#### Override Default Memory and Logging Settings
It is common to have different JVM Memory Arguments and Logging configurations in upstream dev and test environments. The `Advanced` tab allows you override the settings in the Plaform Blueprint. 

![](/Part3/createPlatformModel/img/ModelConfigureAdvanced.PNG)

For the Platform Model we need to specify the following details :
* **WebLogic Admin Server Memory Arguments** - Allows you to specify the JVM Memory arguments for the WebLogic Admin Server.
* **WebLogic Managed Server Memory Arguments** - For each Oracle Middleware Component (for example SOA, OSB and OWSM), allows you to specify the JVM Memory arguments for the WebLogic Managed Server running that component.
* **Logging / Audit Levels for Oracle Middlware Components** - Allows you to specify the Logging / Audti Level for certain Oracle Middleware Components. 

>> Note: The options available will be dependent on which Oracle Middleware components are included within the Platform Blueprint.

Once we have specified the `Genral` and `Advanced` Platform Model configurations, click `Next`.

### Review the Summary

MyST will display a Summary screen showing all the keys inputs specified in the Platform Model Wizard.

![](/Part3/createPlatformModel/img/ModelSummary.PNG)

Once done, click `Finish`. MyST will create the corresponding Platform Model and take you to the Platform Model Editor where you can make additional changes if required. See Editing Platform Models for further details.

## Create Platform Model for AWS On-Demand Infrastructure