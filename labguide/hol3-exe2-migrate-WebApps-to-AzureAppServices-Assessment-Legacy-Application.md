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

1. Search for Azure Migrate, **Azure Migrate** will show you default **Assessment Tools (1)** and **Migration Tools (2)** hyperlinks (You might need to refresh your browser). For the Parts Unlimited website, **App Service Migration Assistant** is the one we need to use. Download links are present on Azure Migrate's Web Apps page. In our case, our lab environment comes with App Service Migration Assistant pre-installed on Parts Unlimited's web server which we will use.

   ![Azure Migrate Web App assessment and migration tools are presented.](Images/App_assiatant_image_machine_installed.png "Azure Migrate Web Apps Capabilities")

1. Goto Azure Portal search for azure migrate, add the tools for assessment and migration via clicking on hyperlinks.
   
    ![Azure Migrate Web App assessment and migration tools are presented.](Images/Azure_App_Migration_Search.png "Azure Migrate Web Apps Capabilities")


   ![Azure Migrate Web App assessment and migration tools are presented.](Images/Click_here_option_to_add_tools.png "Azure Migrate Web Apps Capabilities")


   ![Azure Migrate Web App assessment and migration tools are presented.](Images/click_add_the_tools_on.png "Azure Migrate Web Apps Capabilities")  


![Azure Migrate Web App assessment and migration tools are presented.](Images/After_adding_the_tools.png "Azure Migrate Web Apps Capabilities")  

1. We will use **Azure Migrate: Database Assessment** to assess Parts Unlimited's database hosted on a SQL Server 2008 R2 server. Pick **Azure Migrate: Database Assessment (1)** and select **Add tool (2)**.

    ![Azure Migrate Database Assessment option is selected for Azure Migrate tools. Add tool button is highlighted.](media/updated25.png "Azure Migrate Database Assessment Tools")


1. Under the Azure Migrate umbrella, we now have all of the necessary assessment and migration tools ready for Parts Unlimited.

    ![Azure Migrate databases section is open. Azure Migrate Database Assessment and Database Migration tools are presented.](media/azure-migrate-web-app-6.png "Azure Migrate Database Migration and Assessment Tools")
    

## Summary
 
In this exercise, you have set up Azure Migrate to assess and migrate on-premises servers, infrastructure, applications, and data to Azure.

