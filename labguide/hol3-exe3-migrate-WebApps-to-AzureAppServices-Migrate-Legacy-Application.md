# Lab 3 - Exercise 3: Migrate your application with App Service Migration Assistant

## Lab overview

Azure Migrate is the Powerful tool which helps in assessing the machines readiness to migrate the Azure. this tool helps in migrate the machines, webapps and databases from on premise,hyper-v and different cloud providers.

## Lab scenario

The first step for Parts Unlimited is to assess whether their apps have dependencies on unsupported features on Azure App Service. In this exercise, you use an **Azure Migrate** tool called the App Service migration assistant to evaluate Parts Unlimited's web site for migration to Azure App Service. The assessment runs readiness checks and provides potential remediation steps for common issues. Once the assessment is successful, we will proceed with the migration as well. You will use a simulated on-premises environment hosted in virtual machines running on Azure.

## Lab objectives (Duration: 10 minutes)

In this lab, you will complete the following tasks:
+ Task 1: Perform assessment for migration to Azure App Service.
+ Task 2: Migrate the web application to Azure App Service.

## Task 1: Perform assessment for migration to Azure App Service

Parts Unlimited would like an assessment to see what potential issues they might need to address in moving their application to Azure App Service. You will use the [App Service migration assistant](https://appmigration.microsoft.com/) to assess the application and run various readiness checks.

1. Observe the result of the assessment report. In our case, our application has successfully passed 13 tests with no additional actions needed. Now that our assessment is complete, select **Next** to proceed with migration.

   ![Assessment report result is shown. There are 13 success metrics presented. The next button is highlighted.](Images/assessment_done_will_cehck_afterwards.png "Assessment Report")

   > For the details of the readiness checks, see [App Service Migration Assistant documentation](https://github.com/Azure/App-Service-Migration-Assistant/wiki/Readiness-Checks).

## Task 2: Migrate the web application to Azure App Service

After reviewing the assessment results, you have ensured the web application is a good candidate for migration to Azure App Service. Now, we will continue the process with the migration of the application.

1. In order to continue with the migration of our website, Azure App Service Migration Assistant needs access to our Azure Subscription. Select **Copy Code & Open Browser** button to be redirected to the Azure Portal.

   ![Azure App Service Migration Assistant's Azure Login dialog is open. A device code is presented. Copy Code & Open Browser button is highlighted.](Images/updated31.png "Azure Login")

1. A new tab opens to the login page within the Edge browser. Right-click the text box and select **Paste (1)** to paste your login code. Select **Next (2)** to give subscription access to App Service Migration Assistant.

    ![Azure Code Login web site is open. Context menu for the code textbox is shown. Paste command from the context menu is highlighted. The next button is highlighted as a second step. ](Images/updated32.png "Enter Authentication Code")

1. Continue the login process with your Azure Subscription credentials. When you see the message that says **You have signed in to the Azure App Service Migration Assistant application on your device**, close the browser tab and minimize the Edge browser window to return to the App Service Migration Assistant Window.

    ![Azure Login process is complete. A message dialog is shown that indicates the login process is a success.](Images/updated33.png "App Service Migration Assistant authentication approval")

1. Select the Azure Migrate project we created **(1)** in the previous exercise to submit the results of our migration. Select **Next (2)** to continue.

    ![Azure Migrate Project is set to partsunlimitedweb. The next button is highlighted.](Images/updated34.png "Azure Migrate Hub integration")

1. In order to migrate the Parts Unlimited website, we have to create an App Service Plan. The Azure App Service Migration Assistant will take care of all the requirements needed. Select **Use existing (1)** and select the resource group **Migrate-App-DB-<inject key="DeploymentID" enableCopy="false"/>** **(2)** as your deployment target. App Service requires a globally unique Site Name, enter **partsunlimited-web-<inject key="DeploymentID" enableCopy="false"/>** **(3)** for **Destination Site Name**. Select the **<inject key="location" style="color:red" />** **(4)** region. Click **Migrate** **(5)** to start the migration process.

    ![Deployment options are presented. Existing lab resource group is selected as destination. Destination site name is set to partsunlimited-web-20X21. Migrate button is highlighted.](Images/appservicemigration-migratev2.png "Azure App Service Migration Assistant Options")

   ![Deployment options are presented. Existing lab resource group is selected as destination. Destination site name is set to partsunlimited-web-20X21. Migrate button is highlighted.](Images/congrats_website_migratewd.png "Azure App Service Migration Assistant Options")

    > **WARNING:** If your migration fails with a **WindowsWorkersNotAllowedInLinuxResourceGroup (1)** It may be due to the incorrect region. Try the migration process again, but this time selecting the correct region.  
    >
    > ![Migration failed error screen is shown. WindowsWorkersNotAllowedInLinuxResourceGroup message is highlighted.](Images/updated35.png "Migration failed")

1. We have just completed the migration of the Parts Unlimited website which is hosted on IIS into a Virtual Machine to Azure App Service. Congratulations. Let's go back to the Azure Portal and look into Azure Migrate. Search for `migrate` **(1)** on the Azure Portal and select **Azure Migrate (2)**.*.

    ![Azure Portal is open. The search box is filled with the migrate keyword. Azure Migrate is highlighted from the result list.](Images/updated36.png "Azure Migrate on Azure Portal Search")

1. Switch to the **Web Apps (1)** section. See the number of discovered web servers, assessed websites **(2)** and migrated websites change **(3)**. Keep in mind that you might need to wait for 5 to 10 minutes for the results to show up. You can use the **Refresh** button on the page to see the latest status.

    ![Azure Migrate shows web app assessment and migration reports.](Images/Azure_portal_successful_status.png "Azure Migrate Web Apps Tools")

   ![Azure Migrate shows web app assessment and migration reports.](Images/Migrated_second_proof.png "Azure Migrate Web Apps Tools")

1. Verify the App service being created via migration using App Migration Assistant on azure portal. search for **App Services** click on App Services. if you see the app service being created then the migration is successful.

  ![Azure Migrate shows web app assessment and migration reports.](Images/Check_App_Service_Verify.png "Azure Migrate Web Apps Tools")

   ![Azure Migrate shows web app assessment and migration reports.](Images/Verified_App_Services_Portal.png "Azure Migrate Web Apps Tools")


## Summary
 
In this exercise, you have migrated the on-prem web application to Azure using App Service Migration Assistant. 

