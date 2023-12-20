# Exercise 1: Review the Legacy On-Prem Application

Duration: 10 minutes

In this lab, we have provisioned a web application called **Parts Unlimited**. It is an ASP.NET two-tier application that runs on a windows server with the SQL server back-end and web server front-end.

1. On the Microsoft Edge browser window, enter **localhost** and you will be redirected to the parts Unlimited web application hosted on 
   the web server IIS.

   ![](media/localhost_new.png)
   
2. Go through the web application. We will be migrating this web application from on-prem to Azure App Services in further exercises.

3. From the provided VM, in the search bar, **Search** for **RDP** and **select** the **Remote Desktop Connection** app to verify the 
   database server which will be migrated to the Azure Sql Database.
   
   ![](media/RDP-new.png)

4. Paste the **SQLVM DNS Name** in the **Computer** field and click on **Connect**.
   * **SQLVM DNS Name**: **<inject key="SQLVM DNS Name" style="color:blue" />**

   ![](media/rdp-vm2.png)  
 
5. Now, enter the SQLVM **username**, and **password** provided below and then click on the **Ok** button. Please add the **dot** and **back-slash** “.\” before the username.
   * **username**: **<inject key="SQLVM Username"/>** 
   * **password**: **<inject key="SQLVM Password"/>**
   
   ![](media/vm1-more-choices.png) 

6. Next, click on the **Yes** button to accept the certificate and add in trusted certificates.

   ![](media/logib-vm2-2.png)
   
7. Launch SQL Server Management Studio (SSMS) from the Windows Start menu by typing **"SSMS" (1)** into the search bar, and then select **SQL Server Management Studio 18 (2)** from the search results.

    ![In the Windows Start menu, "sql server management" is entered into the search bar, and SQL Server Management Studio 17 is highlighted in the Windows start menu search results.](media/ssms_search_click_open.png "SQL Server Management Studio 17")
   
8. Connect to your on-premises SQL Database by clicking **Connect** in the Object Explorer.
   
   ![](media/Click_on_Connect.png)
   
9. Once connected, expand the **Databases**, and observe that the database is hosting the **Parts Unlimited** web application.
   
   ![](media/SSMS2.png)
   
10. Close all the windows and disconnect to the remote session of the SQL VM.
   
 Now, click on **Next** in the lab guide section in the bottom right corner to jump to the next exercise instructions.
   
## Summary
 
In this exercise, you have reviewed the legacy on-prem application and database. 

