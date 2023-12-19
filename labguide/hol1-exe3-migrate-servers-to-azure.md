# HOL 1: Migrate Windows and Linux Servers to Azure

Duration: 45 minutes

## Exercise 3: Replicate and Migrate On-premises Virtual Machines to Azure, leveraging Microsoft services and tools including Azure Migrate: Server Migration

### Task 1: Create a Storage Account

In this task you will create a new Azure Storage Account that will be used by Migration and for storage of your virtual machine data during migration.

> **Note:** This lab focuses on the technical tools required for workload migration. In a real-world scenario, more consideration should go into the long-term plan prior to migrating assets. The landing zone required to host VMs should also include considerations for network traffic, access control, resource organization, and governance. For example, the CAF Migration Blueprint and CAF Foundation Blueprint can be used to deploy a pre-defined landing zone, and demonstrate the potential of an Infrastructure as Code (IaC) approach to infrastructure resource management. For more information, see [Azure Landing Zones](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/) and [Cloud Adoption Framework Azure Migration landing zone Blueprint sample](https://docs.microsoft.com/azure/governance/blueprints/samples/caf-migrate-landing-zone/).

1. In the Azure portal's left navigation, select **+ Create a resource**, then search for and select **Storage account**, followed by **Create**.

    ![Screenshot of the Azure portal showing the create storage account navigation.](Images/1.1.png "Storage account - Create")

2. In the **Create storage account** blade, on the **Basics** tab, provide the following values and select **Review (7)**:

   - Subscription: **Select your Azure subscription (1)**.
  
   - Resource group: **MigrateServers (2)**
  
   - Storage account name: **migrationstorage<inject key="DeploymentID" enableCopy="false" /> (3)**

   - Location: Select **<inject key="Region" enableCopy="false" /> (4)** from the dropdown.
    
   - Performance: **Standard (5)**
  
   - Redundancy: **Locally-redundant storage (LRS) (6)**

    ![Screenshot of the Azure portal showing the create storage account blade.](Images/HOL1-EX3-T1-S2-Create-Storage-provide-values.png "Storage account settings")

3. In the review page, select **Create**.

4. Once the storage account is deployed, click on **Go to resource** to open it.

5. Select **Data protection** under **Data management** from the left-hand side menu of storage account.

   ![Screenshot of the Azure portal showing the create storage account blade.](Images/HOL1-EX3-T1-S5-select-data-protection.png)

6. Now, uncheck the box next to **Enable soft delete for blobs** and **Enable soft delete for containers** to disable the soft delete on blobs and container as the soft delete enabled storage account is **not supported** for enabling replication on Virtual Machines. Click on **Save**.

   ![Screenshot of the Azure portal showing the create storage account blade.](Images/1.4.png)

#### Task summary 

In this task you created a new Azure Storage Account that will be used by Migration and modernization.

### Task 2: Register the Hyper-V Host with Migration and modernization

In this task, you will register your Hyper-V host(LabVM) with the Migration and modernization service. This service uses Azure Site Recovery as the underlying migration engine. As part of the registration process, you will deploy the Azure Site Recovery Provider on your Hyper-V host.

1. Return to the **Azure Migrate | Servers, databases and web apps** blade in the Azure Portal, and select **Servers, databases and web apps (1)** under **Migration goals** on the left. Under **Migration Tools**, select **Discover (2)**.

   **Note:** You may need to add the migration tool yourself by following the link below the **Migration Tools** section, selecting **Migration and modernization**, then selecting **Add tool(s)**.
   
     ![Screenshot of the Azure portal showing the 'Discover' button on the Azure Migrate Server Migration panel.](Images/migrationtools.png "Azure Migrate: Server Migration - Discover")

2. In the **Discover** panel, provide the following details:
   - Under **Are your machines virtualized**, select **Yes, with Hyper-V (1)**.
   - Under **Target region (2)** make sure to select the **<inject key="Region"></inject>** region as same the Resource Group's region.
   - Check the **confirmation (3)** checkbox and select **Create resources (4)** to begin the deployment of the Azure Site Recovery resource used by Migration and modernization for Hyper-V migrations.

     ![Screenshot of the Azure portal showing the 'Discover machines' panel from Azure Migrate.](Images/Create_Discover_Resources.png "Discover machines - source hypervisor and target region")

   Once deployment is complete, the 'Discover machines' panel should be updated with additional instructions.
  
3. Click on the **Download** link for the Hyper-V replication provider software installer to download the Azure Site Recovery provider installer.

     ![Screenshot of the Discover machines' panel from Azure Migrate, highlighting the download link for the Hyper-V replication provider software installer.](Images/upd-e3-t2-s3.png?raw=true "Replication provider download link")

4. Return to the **Discover** page in your browser and select the blue **Download** button and download the registration key file.

     ![Screenshot of the Discover machines' panel from Azure Migrate, highlighting the download link Hyper-V registration key file.](Images/upd-e3-t2-s4.png "Download registration key file")


5. Open the **AzureSiteRecoveryProvider.exe** installer you downloaded a moment ago. On the **Microsoft Update** tab, select **Off** and select **Next**. Accept the default installation location and select **Install**.

    > **Note:** If you are prompted with a pop-up like the latest version of the Provider is installed on this server. Would you like to proceed to registration? select **Yes**. (You can directly jump to the next step in that case.)
  
     ![Screenshot of the ASR provider installer.](Images/upd-asr-provider-install.png "Azure Site Recovery Provider Setup")

6. When the installation has completed select **Register**. **Browse (1)** to the location of the key file you downloaded. When the key is loaded select **Next (2)**.

     ![](Images/HOL1-EX3-T2-S6-locate-key-v2.png "Key file registration")

7. Select **Connect directly to Azure Site Recovery without a proxy server (1)** and select **Next (2)**. The registration of the Hyper-V host with Azure Site Recovery will begin.

     ![Screenshot of the ASR provider registration settings.](Images/upd-e3-t2-s8.png)

8. Wait for registration to complete (this may take several minutes). Then select **Finish**.

     ![Screenshot of the ASR provider showing successful registration.](Images/upd-asr-registered.png "Registration complete")

9. Return to the Azure Migrate browser window. **Refresh** your browser, then re-open the **Discover machines** panel by selecting **Discover** under **Migration and modernization** and selecting **Yes, with Hyper-V** for **Are your machines virtualized?**.

10. Select **Finalize registration**, which should now be enabled.

     ![Screenshot of the Discover machines' panel from Azure Migrate, highlighting the download link Hyper-V registration key file.](Images/upd-e3-t2-s10.png?raw=true "Finalize registration")

11. Azure Migrate will now complete the registration with the Hyper-V host. **Wait** for the registration to complete. This may take several minutes.

     ![Screenshot of the 'Discover machines' panel from Azure Migrate, showing the 'Finalizing registration...' message.](Images/upd-discover-6.png "Finalizing registration...")

12. Once the registration is complete, close the **Discover machines** panel using **X** button.

     ![Screenshot of the 'Discover machines' panel from Azure Migrate, showing the 'Registration finalized' message.](Images/upd-discover-7.png "Registration finalized")

13. The **Migration and modernization** panel should now show 5 discovered servers.

     ![Screenshot of the 'Azure Migrate - Servers' blade showing 5 discovered servers under 'Azure Migrate: Server Migration'.](./Images/HOL1-EX3-T2-S13-view-servers-in-modernization-tool.png "Discovered servers")

#### Task summary 

In this task you registered your Hyper-V host with the Azure Migrate Server Migration service.

### Task 3: Enable Replication from Hyper-V to Azure Migrate

In this task, you will configure and enable the replication of your on-premises virtual machines from Hyper-V to the Azure Migrate Server Migration service.

1. Under **Migration and modernization**, select **Replicate**. This opens the **Replicate** wizard.

     ![Screenshot highlighting the 'Replicate' button in the 'Azure Migrate: Server Migration' panel of the Azure Migrate - Servers blade.](Images/HOL1-EX3-T3-S1-select-replicate.png "Replicate link")
   
2. Under **Specific Intent** page, provide the below details:

    -  What do you want to migrate? : Select **Servers or Virtual machines (VM)** **(1)**
    -  Where do you want to migrate to? : Select **Azure VM** **(2)**
    -  Click on **Continue (3)**

     ![](Images/specifi%20intent.png)

3. In the **Basics settings** tab, under **Are your machines virtualized?**, select **Yes, with Hyper-V** from the drop-down. Then select **Next**.

     ![Screenshot of the 'Source settings' tab of the 'Replicate' wizard in Azure Migrate Server Migration. Hyper-V replication is selected.](Images/upd-replicate-2.png "Replicate - Source settings")

4. In the **Virtual machines** tab, under **Import migration settings from an assessment**, select **Yes, apply migration settings from an Azure Migrate assessment (1)**. Select the **Hyper-V VMs (2)** VM group from the dropdown and then select **MigrateServersAssessment (3)** migration assessment.

     ![Screenshot of the 'Virtual machines' tab of the 'Replicate' wizard in Azure Migrate Server Migration. The Azure Migrate assessment created earlier is selected.](Images/HOL1-EX3-T3-S4-select-migrate-group-and-assessment.png "Replicate - Virtual machines")

5. The **Virtual machines** tab should now show the virtual machines included in the assessment. Select the **UbuntuServer** and **WindowsServer (1)** virtual machines, then select **Next (2)**.

     ![Screenshot of the 'Virtual machines' tab of the 'Replicate' wizard in Azure Migrate Server Migration. The UbuntuServer and WindowsServer machines are selected.](Images/HOL1-EX3-T3-S5-select-replication-vms.png "Replicate - Virtual machines")

6. On the **Target settings** tab, select the below information,
   - Select your subscription and the existing **MigrateServers (1)** resource group. 
   - **Replication storage account**: Enter the storage account here from drop down which you create in task 1 **(2)**. 
   - **Virtual Network**: Select **OnPremServerVNet (3)**. 
   - **Subnet**: Select **MigrateSubnet (4)**. 
   - Leave other values as default and select **Next (5)**.
   
     ![Screenshot of the 'Target settings' tab of the 'Replicate' wizard in Azure Migrate Server Migration. The resource group, storage account and virtual network created earlier in this exercise are selected.](Images/HOL1-EX3-T3-S6-replicate-target-settings-tab.png)

   > **Note:** For simplicity, in this lab you will not configure the migrated VMs for high availability, since each application tier is implemented using a single VM.

7. On the **Compute** tab, select the below configuration,
   - Select the **Standard_F2s_v2** VM size for each virtual machine. 
   - Select the **Windows** operating system for the **smarthotelweb1** virtual machines.
   - Select the **Linux** operating system for the **UbuntuWAF** virtual machine. 
   - Select **Next**. 

   ![Screenshot of the 'Compute' tab of the 'Replicate' wizard in Azure Migrate Server Migration. Each VM is configured to use a Standard_F2s_v2 SKU, and has the OS Type specified.](Images/Selecting_replication_os_details.png "Replicate - Compute")
    

8. In the **Disks** tab, review the settings but do not make any changes. Select **Next: Tags**, then select **Replicate** to start the server replication.

9. In the **Azure Migrate - Servers, databases and web apps** blade, under **Migration and modernization**, select the **Overview** button.

     ![Screenshot of the 'Azure Migrate - Servers' blade with the 'Overview' button in the 'Azure Migrate: Server Migration' panel highlighted.](Images/Migration_Overview_page.png "Overview link")
    
10. Confirm that the 2 machines are replicating.

     ![Screenshot of the 'Azure Migrate: Server Migration' overview blade showing the replication state as 'Healthy' for 3 servers.](Images/UPdate_Replication2.png "Replication summary")

11. Select **Replicating Machines (1)** under **Manage** on the left.  Select **Refresh (2)** occasionally and wait until both two machines have a **Protected (2)** status, which shows the initial replication is complete. This will take 5-10 minutes.

     ![Screenshot of the 'Azure Migrate: Server Migration - Replicating machines' blade showing the replication status as 'Protected' for all 2 servers.](Images/Migration_Protected_replication.png "Replication status")

   > **Note**: Please make sure you run the **validation steps** for this task before moving to next tasks as there are few dependencies. **Not** running the validation after performing this task will result in **validation failure** as the status of the Virtual Machine will be changed from **Protected** to **Planned failover** when you migrate the servers in Task5.

#### Task summary 

In this task you enabled replication from the Hyper-V host to Azure Migrate and configured the replicated VM size in Azure.

### Task 4: Configure Networking

In this task you will modify the settings for each replicated VM to use a static private IP address that matches the on-premises IP addresses for that machine.

1. Still using the **Migration and modernization - Replicating machines** blade, select the **WindowsServer** virtual machine. This opens a detailed migration and replication blade for this machine. Take a moment to study this information.

    ![Screenshot from the 'Azure Migrate: Server Migration - Replicating machines' blade with the smarthotelweb1 machine highlighted.](Images/MIgration_Protected_Replication_Windows.png "Replicating machines")

2. Select **Compute and Network (1)** under **General** on the left, then select **Edit (2)**.

    ![Screenshot of the smarthotelweb1 blade with the 'Compute and Network' and 'Edit' links highlighted.](Images/Compute_Pane_edit_1.png "Edit Compute and Network settings")

3. Confirm that the VM is configured to use the **F2s_v2** VM size.

4. Under **Network Interfaces**, select **InternalNATSwitch** to open the network interface settings.

    ![Screenshot showing the link to edit the network interface settings for a replicated VM.](Images/Compute_pane_NAT_EDIT.png "Network Interface settings link")

5. Change the **Private IP address** to **192.168.0.4**

    ![Screenshot showing a private IP address being configured for a replicated VM in ASR.](Images/Compute_Pane_NAT_Update_Edit.png "Network interface - static private IP address")

6. Select **OK** to close the network interface settings blade, then **Save** the **WindowsServer** settings.

7. Repeat these steps to configure the private IP address for the other VMs.
 
   - For **Linux** use private IP address **192.168.0.5**


#### Task summary 

In this task you modified the settings for each replicated VM to use a static private IP address that matches the on-premises IP addresses for that machine

> **Note**: Azure Migrate makes a "best guess" at the VM settings, but you have full control over the settings of migrated items. In this case, setting a static private IP address ensures the virtual machines in Azure retain the same IPs they had on-premises, which avoids having to reconfigure the VMs during migration (for example, by editing web.config files).


### Task 5: Server migration

In this task you will perform a migration of the WindowsServer, redhat machines to Azure.

> **Note**: In a real-world scenario, you would perform a test migration before the final migration. To save time, you will skip the test migration in this lab. The test migration process is very similar to the final migration.

1. Return to the **Migration and modernization** overview blade. Under **Step 3: Migrate**, select **Migrate**.

    ![Screenshot of the 'Azure Migrate: Server Migration' overview blade, with the 'Migrate' button highlighted.](Images/upd-migrate-1.png "Replication summary")

2. On the **Migrate** blade, select **yes (1)** for **Shutdown machines before migration to minimum data loss** and select the 3 virtual machines **(2)** then select **Migrate (3)** to start the migration process.

    ![Screenshot of the 'Migrate' blade, with 3 machines selected and the 'Migrate' button highlighted.](Images/Migrate_Select.png "Migrate - VM selection")

   > **Note**: You can optionally choose whether the on-premises virtual machines should be automatically shut down before migration to minimize data loss. Either setting will work for this lab.

3. The migration process will start.

    ![Screenshot showing 3 VM migration notifications.](Images/upd-migrate-3.png "Migration started notifications")

4. To monitor progress, select **Jobs (1)** under **Manage** on the left and review the status of the three **Planned failover (2)** jobs.

    ![Screenshot showing the **Jobs* link and a jobs list with 3 in-progress 'Planned failover' jobs.](Images/upd-migrate-4.png "Migration jobs")

5. **Wait** until all three **Planned failover** jobs show a **Status** of **Successful**. You should not need to refresh your browser. This could take up to 15 minutes.

    ![Screenshot showing the **Jobs* link and a jobs list with all 'Planned failover' jobs successful.](Images/upd-migrate-5.png "Migration status")

6. Navigate to the **MigrateServers** resource group and check that the VM, network interface, and disk resources have been created for each of the virtual machines being migrated.

    ![Screenshot showing resources created by the test failover (VMs, disks, and network interfaces).](Images/upd-migrate-6.png "Migrated resources")

#### Task summary 

In this task you used Azure Migrate to create Azure VMs using the settings you have configured, and the data replicated from the Hyper-V machines. This migrated your on-premises VMs to Azure.


### Task 6: Verify Migrated Server

Now, to verify the Virtual Machines you migrated. you need to connect to it using bastion service.

1. From the Azure portal menu, which is present at the top left, click on **All services**. Select **compute** from the left-hand menu and select **Virtual machines**.

2. Click on **virtual machine you want to verify**, from the overview blade, and select **Connect**. Select **Bastion** from the available options and click on **Use Bastion**.

     ![Screenshot showing the Azure Bastion connection blade.](Images/USe_Azure_Bastion.png "Connect using Bastion")

   >**Note**: You may have to wait a few minutes and refresh to have the option to enter the credentials. 

3. Connect to the machine with the username **Administrator (1)** and the password **<inject key="SmartHotel Admin Password"></inject> (2)** and then click on **Connect (3)**. When prompted, **Allow** clipboard access.

    >**Note**: You might have to allow pop-ups in order to access the bastion session.

      ![Screenshot showing the Azure Bastion connection blade.](Images/upd-web2-connect.png "Connect using Bastion")

4. After Successful authentication you will be able to connect to the virtual machine on your browser.

      ![Screenshot showing the Azure Bastion connection blade.](Images/Use_Bastion_browser_done.png "Connect using Bastion")
