# Exercise 2: Assessment of Legacy Application using Azure Migrate App Migration Assistant

Duration: 10 minutes

Azure Migrate provides a centralized hub to assess and migrate on-premises servers, infrastructure, applications, and data to Azure. It provides a single portal to start, run, and track your migration to Azure. Azure Migrate comes with a range of tools for assessment and migration that we will use during our lab. We will use Azure Migrate as the central location for our assessment and migration efforts.

1. From the Windows search bar, search for **Default apps** and select it.

   ![Find Default Apps](Images/DefaultApps.png "Find Default Apps")
   
1. On the **Default apps** Blade, click on **Internet Explorer** and select **Microsoft Edge** for setting Microsoft Edge as the default browser.

   ![Edge as default browser](Images/Defaultappsss.png "Set Edge as Default Browser")
   
1. Open the **Azure portal** from the shortcut and log in to Azure. When prompted, use the below credentials to complete the login process.

    * Email/Username: <inject key="AzureAdUserEmail"></inject>
    * Password: <inject key="AzureAdUserPassword"></inject>

    ![Azure Portal shorcut](Images/azure-portal-start.png "Azure Portal shortcut")

1. Once your project is created, **Azure Migrate** will show you default **Web App Assessment (1)** and **Web App Migration (2)** tools (You might need to refresh your browser). For the Parts Unlimited website, **App Service Migration Assistant** is the one we need to use. Download links are present on Azure Migrate's Web Apps page. In our case, our lab environment comes with App Service Migration Assistant pre-installed on Parts Unlimited's web server.

    ![Azure Migrate Web App assessment and migration tools are presented.](media/azure-migrate-web-app-3.png "Azure Migrate Web Apps Capabilities")

1. Another aspect of our migration project will be the database for Parts Unlimited's web site. We will have to assess the database's compatibility and migrate to Azure SQL Database. Let's switch to the **Databases (only) (1)** section in Azure Migrate. Select **Click here (2)** hyperlink for Assessment tools.

    ![Azure Migrate is open. Databases section is selected. Click here link for assessment tools is highlighted.](media/azure-migrate-web-app-4.png "Azure Migrate Databases")

1. We will use **Azure Migrate: Database Assessment** to assess Parts Unlimited's database hosted on a SQL Server 2008 R2 server. Pick **Azure Migrate: Database Assessment (1)** and select **Add tool (2)**.

    ![Azure Migrate Database Assessment option is selected for Azure Migrate tools. Add tool button is highlighted.](media/updated25.png "Azure Migrate Database Assessment Tools")

1. Now, we can see a download link for the **Data Migration Assessment (1)** tool under assessment tools in Azure Migrate. In our case, our lab environment comes with the Data Migration Assessment pre-installed on Parts Unlimited's database server. Select **Click here (2)** under the **Migration Tools** section to continue.

    ![Data Migration Assessment tool's download link is shown. Click here link for migration tools is highlighted.](media/azure-migrate-web-app-5.png "Azure Migrate DMA Download")

1. We will use **Azure Migrate: Database Migration** to migrate Parts Unlimited's database to an Azure SQL Database. Pick **Azure Migrate: Database Migration (1)** and select **Add tool (2)**.

    ![Azure Migrate Database Migration option is selected for Azure Migrate tools. Add tool button is highlighted.](media/updated26.png "Azure Migrate Database Migration Tool")

1. Under the Azure Migrate umbrella, we now have all of the necessary assessment and migration tools ready for Parts Unlimited.

    ![Azure Migrate databases section is open. Azure Migrate Database Assessment and Database Migration tools are presented.](media/azure-migrate-web-app-6.png "Azure Migrate Database Migration and Assessment Tools")
    

## Summary
 
In this exercise, you have set up Azure Migrate to assess and migrate on-premises servers, infrastructure, applications, and data to Azure.

