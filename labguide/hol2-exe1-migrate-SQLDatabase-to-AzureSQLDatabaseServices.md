# Exercise 4: Migrate the on-premises database to Azure SQL Database

Duration: 55 minutes

The next step of Part Unlimited's migration project is the assessment and migration of its database. Currently, the database lives on SQL Server 2008 R2 on a virtual machine. You will use an **Azure Migrate: Database Assessment** tool called **Microsoft Data Migration Assistant (DMA)** to assess the `PartsUnlimited` database for migration to Azure SQL Database. The assessment generates a report detailing any feature parity and compatibility issues between the on-premises database and Azure SQL Database. After the assessment, you will use an **Azure Migrate: Database Migration** service called **Azure Database Migration Service (DMS)**. During the exercise, you will use a simulated on-premises environment hosted on virtual machines running on Azure.

## Task 1: Connect to your SqlServer2008 VM with RDP

1. From your lab environment (**WebVM**), in the search bar, **Search** for **RDP** and **select** the **Remote Desktop Connection** app.
   
   ![](Images/RDP-new.png)

2. Paste the **SQLVM DNS Name** in the **Computer** field and click on **Connect**.
   * **SQLVM DNS Name**: **<inject key="SQLVM DNS Name" style="color:blue" />**

   ![](Images/rdp-vm2.png)  
 
3. Now, enter the SQLVM **username**, and **password** provided below and then click on the **Ok** button. Please add the **dot** and **back-slash** “.\” before the username.
   * **username**: **<inject key="SQLVM Username" style="color:blue" />** 
   * **password**: **<inject key="SQLVM Password" style="color:blue" />**
   
   ![](Images/vm1-more-choices.png) 

4. Next, click on the **Yes** button to accept the certificate and add in trusted certificates.

   ![](Images/logib-vm2-2.png)

## Task 2: Perform assessment for migration to Azure SQL Database

Parts Unlimited would like an assessment to see what potential issues they might need to address in moving their database to Azure SQL Database. In this task, you will use the [Microsoft Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) (DMA) to assess the `PartsUnlimited` database against Azure SQL Database (Azure SQL DB). Data Migration Assistant (DMA) enables you to upgrade to a modern data platform by detecting compatibility issues that can impact database functionality on your new version of SQL Server or Azure SQL Database. It recommends performance and reliability improvements for your target environment. The assessment generates a report detailing any feature parity and compatibility issues between the on-premises database and the Azure SQL DB service.

> **Note**: The Database Migration Assistant is already installed on your Lab (Web) VM. If not found, it can be downloaded through Azure Migrate or from the [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=2090807) as well, and as Data Migration Assistant is dependent on .NET Framework 4.8 download and install .Net Framework from [here](https://go.microsoft.com/fwlink/?LinkId=2085155) and **restart** the VM before you install Data Migration Assistant.

1. Launch DMA from the Windows desktop Screen **Microsoft Data Migration assistant**.

    > **Note**: There is a known issue with screen resolution when using an RDP connection to Windows Server 2008 R2, which may affect some users. This issue presents itself as very small, hard to read text on the screen. The workaround for this is to use a second monitor for the RDP display, which should allow you to scale up the resolution to make the text larger.

   ![In the Windows Start menu, "data migration" is entered into the search bar, and Microsoft Data Migration Assistant is highlighted in the Windows start menu search results.](Images/DMA-01-ICON-SHOW.png "Data Migration Assistant")

2. In the DMA dialog, select **+** from the left-hand menu to create a new project.

   ![The new project icon is highlighted in DMA.](Images/updated38.png "New DMA project")

3. In the New Project pane, set the name of the **project** and make sure the following values are selected:

   - **Project type**: Select Assessment.
   - **Project name**: Enter **Assessment**
   - **Assessment type**: Select Database Engine.
   - **Source server type**: Select SQL Server.
   - **Target server type**: Select Azure SQL Database.
   - Select **Create**.

   ![New project settings for doing an assessment of a migration from SQL Server to Azure SQL Database.](Images/updated39.png "New project settings")

4. On the **Options** screen, ensure **Check database compatibility** and **Check feature parity** are both checked, and then select **Next**.

   ![Check database compatibility and check feature parity are checked on the Options screen.](Images/appmod-EX3s4.png "DMA options")

5. On the **Sources** screen, enter the following into the **Connect to a server** dialog that appears on the right-hand side:

    - **Server name**: Enter **SQLSERVER2008**
    - **Authentication type**: Select **SQL Server Authentication**.
    - **Username**: Enter **PUWebSite**
    - **Password**: Enter **<inject key="SQLVM Password" />**
    - **Encrypt connection**: Check this box if not checked.
    - **Trust server certificate**: Check this box.
    - Select **Connect**.

    ![In the Connect to a server dialog, the values specified above are entered into the appropriate fields.](Images/updated40.png "Connect to a server")

6. In the **Add sources** dialog that appears next, check the box for `PartsUnlimited` **(1)** and select **Add (2)**.

    ![The PartsUnlimited box is checked on the Add sources dialog.](Images/updated41.png "Add sources")

7. Select **Start Assessment**.

    ![Start assessment](Images/dma-start-assessment-to-azure-sql-db.png "Start assessment")

8. Take a moment to review the assessment for migrating to Azure SQL DB. The SQL Server feature parity report shows that Analysis Services and SQL Server Reporting Services are unsupported, but these do not affect any objects in the `PartsUnlimited` database, so we won't block a migration. If there is no SQL Server feature parity, then proceed to the next step.

    ![The feature parity report is displayed, and the two unsupported features are highlighted.](Images/app-mod-new.png "Feature parity")

9. Now, select **Compatibility issues (1)** to review that report as well.

    ![The Compatibility issues option is selected and highlighted.](Images/updated42.png "Compatibility issues")

    The DMA assessment for migrating the `PartsUnlimited` database to a target platform of Azure SQL DB reveals that no issues or features are preventing Parts Unlimited from migrating their database to Azure SQL DB.

10. Select **Upload to Azure Migrate** to upload assessment results to Azure.

    ![Upload to Azure Migrate button is highlighted.](Images/dma-upload-azure-migrate.png "Azure Migrate Upload")

11. Select the right Azure environment your subscription lives. Select **Connect** to proceed to the Azure login screen. Please use the  below credentials to login.
    * Email/Username: <inject key="AzureAdUserEmail"></inject>
    * Password: <inject key="AzureAdUserPassword"></inject>

    ![Azure is selected as the Azure Environment on the connect to Azure screen. Connect button is highlighted.](Images/dma-azure-migrate-upload.png "Azure Environment Selection")

12. Select your **subscription** and the **partsunlimitedweb-XXXXXX**` Azure Migrate project you created earlier to migrate the server and webapps. Select **Upload** to start the upload to Azure.

    ![Upload to Azure Migrate page is open. Lab subscription and partsunlimited Azure Migrate Project are selected. Upload button is highlighted.](Images/dma.png "Azure Migrate upload settings")


13. Once the upload is complete, select **OK** and navigate to the Azure Migrate page on the Azure Portal.

    ![Assessment Uploaded dialog shown.](Images/updated43.png "Assessment Uploaded")

14. Select the **Databases (only)** option on Azure Migrate page. Observe the number of assessed database instances and the number of databases ready for **Azure SQL DB**. Keep in mind that you might need to wait for 5 to 10 minutes for the results to show up. You can use the **Refresh** button on the page to see the latest status.

    ![Azure Migrate Databases page is open. The number of assessed database instances and the number of databases ready for Azure SQL DB shows one.](Images/updated_verify_sql_database_above_migrate_project.png "Azure Migrate Database Assessment")

## Task 3: Retrieve connection information for SQL Databases (Optional)

In this task, you will retrieve the Fully Qualified Domain Name for the Azure SQL Database. This information is needed to connect to the Azure SQL Database from Azure Data Migration Service and Azure Data Migration Assistant.

1. In the [Azure portal](https://portal.azure.com), navigate to your resource group containing the lab resources and **SQL database** resource by selecting the **parts** SQL database resource from the resources list.

   ![The parts SQL database resource is highlighted in the list of resources.](Images/Click_on_SQl_Database_azure.png "SQL database")

2. On the **Overview** Blade of your SQL database, copy the **Server name** and paste the value into a text editor, such as Notepad.exe, for later reference.

   ![The server name value is highlighted on the SQL database Overview blade.](Images/Copu_DNS_Name_SQL_Database.png "SQL database")

## Task 4: Migrate the database schema using the Data Migration Assistant

After you have reviewed the assessment results and you have ensured the database is a candidate for migration to Azure SQL Database, please use the Data Migration Assistant to migrate the schema to Azure SQL Database.

1. Return to the Data Migration Assistant, and select the New **(+)** icon in the left-hand menu.

2. In the New project dialog, enter the following:

   - **Project type**: Select Migration.
   - **Project name**: Enter **Migration**
   - **Source server type**: Select SQL Server.
   - **Target server type**: Select Azure SQL Database.
   - **Migration scope**: Select Schema only.
   - Select **Create**.

   ![The above information is entered in the New project dialog box.](Images/updated46.png "New Project dialog")

3. On the **Select source** tab, enter the following:

   - **Server name**: Enter **SQLSERVER2008**.
   - **Authentication type**: Select **SQL Server Authentication**.
   - **Username**: Enter **PUWebSite**
   - **Password**: Enter **<inject key="SQLVM Password" />**
   - **Encrypt connection**: Check this box.
   - **Trust server certificate**: Check this box.
   - Select **Connect**, and then ensure the `PartsUnlimited` database is selected from the list of databases.
   - Select **Next**.

   ![The Select source tab of the Data Migration Assistant is displayed, with the values specified above entered into the appropriate fields.](Images/updated47.png "Data Migration Assistant Select source")

4. On the **Select target** tab, enter the following:

   - **Server name**: Enter the server name of your Azure SQL Database - **<inject key="sqlDatabaseName" enableCopy="false"/>.database.windows.net** 
   - **Authentication type**: Select SQL Server Authentication.
   - **Username**: Enter **demouser**
   - **Password**: Enter **<inject key="SQLVM Password" />**
   - **Encrypt connection**: Check this box.
   - **Trust server certificate**: Check this box.
   - Select **Connect**, and then ensure the `parts` database is selected from the list of databases.
   - Select **Next**.

   ![The Select target tab of the Data Migration Assistant is displayed, with the values specified above entered into the appropriate fields.](Images/Migratino_checllist_signinto_targetr.png "Data Migration Assistant Select target")

5. On the **Select objects** tab, leave all the objects checked, and select **Generate SQL script**.

    ![The Select objects tab of the Data Migration Assistant is displayed, with all the objects checked.](Images/data-migration-assistant-migration-select-objects.png "Data Migration Assistant Select target")

6. On the **Script & deploy schema** tab, review the script. Now, select **Deploy schema**.

    ![The Script & deploy schema tab of the Data Migration Assistant is displayed, with the generated script shown.](Images/data-migration-assistant-migration-script-and-deploy-schema.png "Data Migration Assistant Script & deploy schema")

7. After the schema is deployed, review the deployment results, and ensure there are no errors.

    ![The schema deployment results are displayed, with 23 commands executed and 0 errors highlighted.](Images/updated48.png "Schema deployment results")

8. Launch SQL Server Management Studio (SSMS) from the Windows Start menu by typing "SSMS" into the search bar, and then selecting **SQL Server Management Studio 18** in the search results.

    ![In the Windows Start menu, "sql server management" is entered into the search bar, and SQL Server Management Studio 17 is highlighted in the Windows start menu search results.](Images/ssms_search_click_open.png "SQL Server Management Studio 17")

9. Connect to your Azure SQL Database, by selecting **Connect->Database Engine** in the Object Explorer, and then enter the following into the Connect to server dialog:

    - **Server name**: Enter the server name of your Azure SQL Database - **<inject key="sqlDatabaseName" enableCopy="false"/>.database.windows.net** 
    - **Authentication type**: Select SQL Server Authentication.
    - **Login**: Enter **demouser**
    - **Password**: Enter **<inject key="SQLVM Password" />**
    - **Remember password**: Check this box.
    - Select **Connect**.

    ![The SSMS Connect to Server dialog is displayed, with the Azure SQL Database name specified, SQL Server Authentication selected, and the demouser credentials entered.](Images/conect_to_azure_sql_using_mysql.png "Connect to Server")

10. Once connected, expand **Databases**, and expand **parts**, then expand **Tables**, and observe the schema that has been created. Expand **Security > Users** to observe that the database user is migrated as well.

    ![In the SSMS Object Explorer, Databases, parts, and Tables are expanded, showing the tables created by the deploy schema script. Security Users are expanded to show database user PUWebSite is migrated as well.](Images/Verify_Database_Connecting_.png "SSMS Object Explorer").

> **Note**: You can now disconnect from the **SQLVM** and perform the remaining exercises from the **LabVM**.

## Task 5: Migrate the database using the Azure Database Migration Service

At this point, you have migrated the database schema using DMA. In this task, you migrate the data from the `PartsUnlimited` database into the new Azure SQL Database using the Azure Database Migration Service.

> The [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) integrates some of the functionality of Microsoft's existing tools and services to provide customers with a comprehensive, highly available database migration solution. The service uses the Data Migration Assistant to generate assessment reports that provide recommendations to guide you through the changes required prior to performing a migration. When you're ready to begin the migration process, Azure Database Migration Service performs all of the required steps.

1. In the [Azure portal](https://portal.azure.com), navigate to your DMS (Data Migration Service) by searching Azure Database Migration Service on azure search.

   ![The contoso-dms Azure Database Migration Service is highlighted in the list of resources in the hands-on-lab-SUFFIX resource group.](Images/searchingon_azure_database_azure.png "Resources")

1. On the Azure Database Migration Service Blade, select **Create**.

   ![On the Azure Database Migration Service blade, +New Migration Project is highlighted in the toolbar.](Images/Search_Azure_Database_Migration_Assistant.png "Azure Database Migration Service New Project")


3. On the New create Blade, enter the following:

   - **Source server type**: Select SQL Server.
   - **Target server type**: Select Azure SQL Database.
   - **Database Migration Service**: Select **Database Migration Service**
   - Select **Select**.

   ![The New migration project blade is displayed, with the values specified above entered into the appropriate fields.](Images/Select_DMS_Assistant_Create.png "New migration project")

4. On the Migration Wizard **Select source** Blade, enter the following:

   - **Source SQL Server instance name (1)**: Enter the SQL DNS name - **<inject key="SQLVM DNS Name" enableCopy="true"/>** 
   - **Authentication type (2)**: Select SQL Authentication.
   - **Username (3)**: Enter **PUWebSite**
   - **Password (4)**: Enter **<inject key="SQLVM Password" />**
   - **Connection properties (5)**: Check both Encrypt connection and Trust server certificate.
   - Select **Next: Select databases >> (6)**.

   ![The Migration Wizard Select source blade is displayed, with the values specified above entered into the appropriate fields.](media/dms.png "Migration Wizard Select source")

5. The PartsUnlimited databases comes preselected. Select **Next: Select target >>** to continue.

    ![The Migration Wizard Select database blade is displayed. PartsUnlimited databases is selected. Next: Select target >> button is highlighted.](media/updated54.png "Migration Wizard Select databases")

6. On the Migration Wizard **Select target** Blade, enter the following:

   - **Target server name (1)**: Enter the server name of your Azure SQL Database - **<inject key="sqlDatabaseName" enableCopy="false"/>.database.windows.net**
   - **Authentication type (2)**: Select SQL Authentication.
   - **Username (3)**: Enter **demouser**
   - **Password (4)**: Enter **<inject key="SQLVM Password" />**
   - **Connection properties**: Check Encrypt connection.
   - Select **Next: Map to target databases >> (5)**.

   ![The Migration Wizard Select target blade is displayed, with the values specified above entered into the appropriate fields.](media/updated55.png "Migration Wizard Select target")

7. On the Migration Wizard **Map to target databases** Blade, confirm that **PartsUnlimited (1)** is checked as the source database, and **parts (2)** is the target database on the same line, then select **Next: Configuration migration settings >> (3)**.

    ![The Migration Wizard Map to target database blade is displayed, with the ContosoInsurance line highlighted.](media/updated56.png "Migration Wizard Map to target databases")

8. On the Migration Wizard **Configure migration settings** Blade, expand the **PartsUnlimited (1)** database, verify all the tables are selected **(2)** and select **Next: Summary >> (3)**.

    ![The Migration Wizard Configure migration settings blade is displayed, with the expand arrow for PartsUnlimited highlighted, and all the tables checked.](media/updated57.png "Migration Wizard Configure migration settings")

9. On the Migration Wizard **Summary** Blade, enter the following:

    - **Activity name (1)**: Enter ``PartsUnlimitedDataMigration``
    - Select **Start migration (2)**.

    ![The Migration Wizard summary blade is displayed, with PartsUnlimitedDataMigration entered into the name field.](media/updated58.png "Migration Wizard Summary")


10. Monitor the migration on the status screen that appears. Select the refresh icon in the toolbar to retrieve the latest status.

    ![On the Migration job blade, the Refresh button is highlighted, and a status of Full backup uploading is displayed and highlighted.](media/updated59.png "Migration status")

    > The migration takes approximately 2 - 3 minutes to complete.

11. When the migration is complete, you should see the status as **Completed**.

    ![On the Migration job blade, the status of Completed is highlighted.](media/updated60.png "Migration with Completed status")

12. When the migration is complete, select the **PartsUnlimited** migration item.

    ![The ContosoInsurance migration item is highlighted on the PartsUnlimitedDataMigration blade.](media/updated61.png "PartsUnlimitedDataMigration details")

13. Review the database migration details.

    ![A detailed list of tables included in the migration is displayed.](media/updated62.png "Database migration details")

14. If you received a status of "Warning" for your migration, you can find more details by selecting **Download report** from the ContosoDataMigration screen.

    ![The Download report button is highlighted on the DMS Migration toolbar.](media/updated63.png "Download report")

    > **Note**: The **Download report** button will be disabled if the migration is completed without warnings or errors.

    The reason for the warning can be found in the Validation Summary section. In the report below, you can see that a storage object schema difference triggered a warning. However, the report also reveals that everything was migrated successfully.            

    ![The output of the database migration report is displayed.](media/dms-migration-wizard-report.png "Database migration report")

## Task 6: Configure the application connection to SQL Azure Database

Now that we have both our application and database migrated to Azure. It is time to configure our application to use the SQL Azure Database.

1. In the [Azure portal](https://portal.azure.com), navigate to your `parts` SQL Database resource by selecting **Resource groups** from Azure services list, selecting the **hands-on-lab-<inject key="DeploymentID" enableCopy="false"/>** resource group, and selecting the `parts` SQL Database from the list of resources.

   ![The parts SQL database resource is highlighted in the list of resources.](media/updated64.png "SQL database")

2. Switch to the **Connection strings (1)** Blade, and copy the connection string under **ADO.NET(SQL authentication)** by selecting the copy button **(2)**.

   ![Connection string panel if SQL Database is open. Copy button for ADO.NET connection string is highlighted.](media/appmod-ex4-t6-s2.png "Database connection string")

3. Paste the value into a text editor, such as Notepad.exe, to replace the Password placeholder. Replace the `{your_password}` section with **<inject key="SQLVM Password" />**. Copy the full connection string with the replaced password for later use.

    ![Notepad is open. SQL Connection string is pasted in. {your_password} placeholder is highlighted.](media/sql-connection-string-password-replace.png "Database connection string")

4. Go back to the resource list, navigate to your partsunlimited-web-<inject key="DeploymentID" enableCopy="false"/> **(2)** App Service resource. You can search for `partsunlimited-web` **(1)** to find your Web App and App Service Plan.

   ![The search box for resources is filled in with partsunlimited-web. The partsunlimited-web-20 Azure App Service is highlighted in the list of resources in the hands-on-lab-SUFFIX resource group.](media/updated66.png "Resources")

5. Switch to the **Configuration (1)** Blade, and select **+New connection string (2)**.

    ![App service configuration panel is open. +New connection string button is highlighted.](media/updated67.png "App Service Configuration")

6. On the **Add/Edit connection string** panel, enter the following:

   - **Name (1)**: Enter `DefaultConnectionString`
   - **Value (2)**: Enter SQL Connection String you copied in Step 3.
   - **Type (3)**: Select **SQLAzure**
   - **Deployment slot setting (4)**: Check this option to make sure connection strings stick to a deployment slot. This will be helpful when we add additional deployment slots during the next exercises.
   - Select **OK (5)**.

    ![Add/Edit Connection string panel is open. Name field is set to DefaultConnectionString. Value field is set to the connection string copied in a previous step. Type is set to SQL Azure. Deployment slot setting checkbox is checked. The OK button is highlighted. ](media/updated68.png "Adding connection string")

7. Select **Save** and **Continue** for the following confirmation dialog.

    ![App Service Configuration page is open. Save button is highlighted.](media/updated69.png "App Service Configuration")

8. Switch to the **Overview (1)** Blade, and select **Default domain (2)** to navigate to the Parts Unlimited web site hosted in our Azure App Service using Azure SQL Database.

    ![Overview panel for the App Service is on screen. URL for the app service if highlighted.](media/appmod-ex4-t6-s8.png "App Service public URL")
    
    
 ## Summary
 
In this exercise, you have migrated the on-premises database to Azure SQL Database.
