---
page_type: sample
languages: 
- csharp
products: 
- azure
- azure-event-hubs
- cloud-services
- sql-database
description: "How to take data from SQL to Event Hub with .NET."
urlFragment: SQL to Event Hub
author: spyrossak
---

# How to take data from SQL to Event Hub with .NET

## SDK Versions
In this sample,you will find the following folders:
* **SBv2** - references Service Bus SDK v2
* **EHv5** - references Event Hub SDK v5

## Prerequisites

To complete this tutorial:

* Install .NET Core latest version for [Linux] or [Windows]

If you don't have an Azure subscription, create a [free account] before you begin.

### Create a SQL Database using the Azure portal

Step 1 : Create a new Event Hub Namespace to use for this tutorial.

*  Go to the [Azure Portal] and log in using your Azure account.
*  Select **New** > **Databases** > **SQL Database**.
*  Select your Subscription.
*  For `Resource group`, create a new one and give it a unique name.
*  Enter a name for your Database.
*  Select the `Server` to use for your SQL Database.
*  Check **Review + create** and click **Create** to create your SQL Database.

Step 2 : Copy and save Connection string.
 
After your SQL database is created. Click on it to open it. 
Select **Settings** > **Properties** > **Show database connection strings**, Copy the first one, then paste it into a text editor for later use.

### Create an Event Hub using the Azure portal

Step 1 : Create a new Event Hub Namespace to use for this tutorial.

*  Go to the [Azure Portal] and log in using your Azure account.
*  Select **New** > **Event Hubs** > **Create**.
*  Enter a name for your Event Hub Namespace.
*  Set `Pricing tier` to **Standard**.
*  Select your Subscription.
*  For `Resource group`, create a new one and give it a unique name.
*  Select the `Location` to use for your Event Hub Namespace.
* Click **Create** to create your Event Hub Namespace.

Step 2: Create a new Event Hub to use for this tutorial.

*  Go to the Event Hub Namespace just created.
*  Select **Entities** > **Event Hubs** > **Event Hub**.
*  Enter a name for your Event Hub.
*  Click **Create** to create your Event Hub.

Step 3 : Copy and save connection sring.

After your Event Hub is created. Click on it to open it. 
Select **Settings** > **Shared access policies** > **RootManageSharedAccessKey** > **Connection string–primary key / Connection string–secondary key**, Select a connection string and copy the **connection string** to the clipboard, then paste it into text editor for later use.

## Run the application
First, clone the repository on your machine:

```bash
git clone https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql.git
```

Second, switch to the appropriate folder(SBv2/EHv5).

Then, edit App.config in the SqlToEventHub folder to provide the relevant source and target configuration data.
* Find the key **sqlDatabaseConnectionString** in the ```<appSettings>``` section, Replace the value with the connection string to the SQL database.
* Find the key **DataTableName** in the ```<appSettings>``` section, Replace the value with the name of your table (without the ```dbo.``` prefix).
* Find the key **OffsetKey** in the ```<appSettings>``` section, Replace the value with the name of that field in your table.
* Find the key **SleepTimeMs** in the ```<appSettings>``` section, Replace Replace ```10000``` with the interval that you want to use.
* Find the key **Microsoft.Azure.EventHubToUse** in the ```<appSettings>``` section, Replace the value with the name of the event hub that you created.
* Find the key **Microsoft.Azure.ConnectionString** in the ```<appSettings>``` section, Replace the value with the whole of the string that you copied from the portal.

Finally, open `SqlToEventHub.sln` with Visual Studio, and run the application.

## This sample shows how to do following operations of Event Hub
This section describes: This sample deals with the opposite, taking data out of SQL and pushing it to an Event Hub.
- Create a SQL database using the Auzre Portal.
- Create an Event Hub using the Auzre Portal.
- Create an Event Hub Producer Client.
- Publish events from SQL database to the Event Hub
  - In Visual Studio, right-click on 'WorkerRole' in Solution 'SqlToEventHub', and select *Publish*.
  - In the Publish Azure Application, answer the following questions. 
    - Name: [pick something unique]
    - Region: [pick same region as you used for the Event Hub]
    - Database server: no database
    - Database password: [leave suggested password]
  - Click Publish, and wait until the status bar shows "Completed". At that point the application is running in your subscription, polling the SQL table for any records that have been added since the last time it was polled, and pushing those records to your Event Hub. 

## More information

For more information about this sample, see the [Pulling data from SQL into an Azure Event Hub] topic in this repository.

<!-- LINKS -->
[Linux]: https://dotnet.microsoft.com/download
[Windows]: https://dotnet.microsoft.com/download
[free account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F
[Azure Portal]: https://portal.azure.com
[Pulling data from SQL into an Azure Event Hub]: (https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql/blob/master/event-hubs-pulling-sql-data.md)