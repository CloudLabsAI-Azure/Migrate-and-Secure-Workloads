# Migrate & Secure Workloads  

## Overview

Before the lab, you will have pre-deployed an on-premises infrastructure hosted in Hyper-V.  This infrastructure is hosting a multi-tier application called 'SmartHotel', using Hyper-V VMs for each of the application tiers. you will also be securing the migrated workload using Defender for cloud and using Sentinel for Incidents and events management system

During the lab, you will migrate this entire application stack to Azure. This will include assessing the on-premises application using Azure Migrate; assessing the database migration using Microsoft Data Migration Assistant (DMA); migrating the database using the Azure Database Migration Service (DMS); and migrating the web and application tiers using Azure Migrate: Server Migration. This includes migration of both Windows and Linux VMs. using Azure Defender for Cloud you will be onboarding and securing the machines and incidents, event management will be tracked using the Azure Sentinel 

## Key features of Azure Migrate, Azure Defender for Cloud and Azure Sentinel

- **Database tier** Hosted on the SQLVM, which is running Windows Server.

- **Application tier** Hosted on the smarthotel, which is running Windows Server.

- **Web tier** Hosted on the WEBVM VM, which is running Windows Server.

- **Web proxy** Hosted on the  UbuntuWAF VM, which is running Nginx on Ubuntu.

For simplicity, there is no redundancy in any of the tiers.

>**Note:** For convenience, the Hyper-V host itself is deployed as an Azure VM. For the purposes of the lab, you should think of it as an on-premises machine.

![A slide shows the on-premises SmartHotel application architecture. This comprises a SmartHotelHost server running Microsoft Hyper-V. This server hosts 4 VMs: UbuntuWAF, SmartHotelWeb1, SmartHotelWeb2, and SmartHotelSQL1. A series of arrows show how these VMs will be migrated to Azure. The first 3 VMs have an arrow labeled 'Azure Migrate: Server Migration' pointing to 3 similarly-labeled VMs in Azure. The last VM, SmartHotelSQL1, has an arrow labeled 'Azure Database Migration Service' pointing to an Azure SQL Database. A third arrow labeled 'Azure Migrate: Server Assessment' and 'Data Migration Assistant (DMA)' points from all 4 on-premises VMs to an Azure Migrate dashboard showing migration readiness.](Images/overview.png "SmartHotel Migration Overview")

Throughout this lab, you will use Azure Migrate as your primary tool for assessment and migration. In conjunction with Azure Migrate, you will also use a range of other tools, as detailed below.

To assess the Hyper-V environment, you will use Azure Migrate: Server Assessment. This includes deploying the Azure Migrate appliance on the Hyper-V host to gather information about the environment. For deeper analysis, the Microsoft Monitoring Agent and Dependency Agent will be installed on the VMs, enabling the Azure Migrate dependency visualization.

The SQL Server database will be assessed by installing the Microsoft Data Migration Assistant (DMA) on the Hyper-V host, and using it to gather information about the database. Schema migration and data migration will then be completed using the Azure Database Migration Service (DMS).

The application, web, and web proxy tiers will be migrated to Azure VMs using Azure Migrate: Server Migration. You will walk through the steps of building the Azure environment, replicating data to Azure, customizing VM settings, and performing a failover to migrate the application to Azure.

> **Note**: After migration, the application could be modernized to use Azure Application Gateway instead of the Ubuntu Nginx VM, and to use Azure App Service to host both the web tier and application tiers. These optimizations are out of scope of this lab, which is focused only on a 'lift and shift' migration to Azure VMs.

Azure Defender for Cloud, you will be using to onboard the machine to security platform which is Defender for cloud. it helps in Advance Threat Protection, Threat Intelligence, incident reports, integration with azure policy to secure the Workload environment.

Azure Sentinel will be using as Security Information and Event Management, Threat Intelligence Integration, Incident Detection and Investigation and Playbooks and Automation as it provides centralized view for security operations and incident response across an organization.


## Sandbox Scenario

Smathotel is a global organization with a complex IT infrastructure that includes a combination of hyper-v machines and cloud-based resources for another website partsunlimited. They are looking to migrate the machines, webapp and database to azure. and also want to enhance their security posture by deploying Azure Sentinel, and Azure Defender for Cloud. Microsoft's  sentinel is a cloud-native security information and event management (SIEM), and security orchestration automation and response (SOAR) solution. Additionally, Contoso aims to onboard its cloud resources and servers to Azure Sentinel to gain better visibility and proactive threat detection and response capabilities using the Azure Defender for Cloud.

By implementing a robust Log analytics and threat detection program, Contoso aims to proactively identify and mitigate threats, reduce the risk of security breaches, and maintain a strong security posture in an ever-evolving threat landscape. This approach will enable Contoso to stay ahead of potential threats and protect its digital assets effectively.

## About the Sandbox

Using this environment, You'll be able to explore complete features and offerings listed. Please find the detailed overview of the sandbox environment below.

### Pre-provisioned resources

#### **Virtual Machines**: 

- 2 *Windows Server Datacenter* Virtual machines for webapps and SQl server and database, and 1 *Windows Server Datacenter* Virtual Machine with Hyper-V and machines create and configured to use. virtual machine-related resources like Virtual networks, Network security groups, managed disks, Network interface cards, and IP addresses are deployed as part of the automation.

  You are recommended to use the same virtual machine throughout the lab for the best experience through out the lab.

#### **License and subscription**: 

- You'll have access to a pre-configured Microsoft user account with an active Azure subscription, a tenant, and a Microsoft 365 E5 license assigned to the user. 
   
  User account has assigned as Owner at subscription and Global administrator at the tenant level. You need to use the same user account throughout the lab to get the most out of the lab. 

#### **Azure Credits**: 

- You have been given a quota of **$150 USD** which includes the running cost of Pre-deployed resources, license cost, and other resources deployed while running through the lab.

  You will receive **cost alerts** to your registered email address at **50%/75%/90%/95%/100%** of the allotted Azure Credit is spent.

  You can visit the Azure Subscription page to check the current Azure credit spend and Analysis on **Cost analysis** tab under the Cost Management option.

  ![Picture 1](Images/o1.jpg)

#### **Duration and Deletion of sandbox**:  

- The sandbox environment will be active for **30 days/730** hours from the time of registration. 
- The allowed uptime of the virtual machine is **40 hours**.
- The virtual machines will automatically **shut down** if not in use or if virtual machines are left idle. This feature is enabled in virtual machines to minimize the Azure spend.
- when 100% of Azure credits are spent, the sandbox environment will get automatically deleted without any prior notification. To retain the environment for a longer period and to get the most out of the environment, please follow the best practices mentioned below.

#### **Best practices**: 

- **Resources usage**: Please stop the virtual machines and other resources when not in use in order to minimize the Azure spend.

- **Azure Cost Analysis**: Maintain a practice of checking the Cost Analysis report of the assigned Azure subscription oftenly in check the Azure spend so that enviornment for a longer duration of time.

- **Alert notifications**: Make sure to check your registered email's inbox for any alert-related mails. Alerts give you can head start to keep your Azure spending in control and to plan out the remaining credits in the best way possible.

## Lab guide Content:

You will have access to a lab guide which is a reference material to assist you in getting started with the exploration. You are encouraged to explore Microsoft Purview further based on your interests and preferences.

- hol1
  - exe1 - create setup azure migrate
  - exe2 - discover assess workloads with appliance
  - exe3 - migrate servers to azure
- hol2
  - exe1 - migrate SQLDatabase to AzureSQLDatabaseServices 
- hol3
  - exe1 - migrate WebApps to AzureAppServices Review Legacy App Database
  - exe2 - migrate WebApps to AzureAppServices Assessment Legacy Application
  - exe3 - migrate WebApps to AzureAppServices Migrate Legacy Application
- hol4
  - exe1 - Secure Workloads with Defender for Cloud
- hol5
  - exe1 - SIEM with Sentinel

### Azure services and related products

- Log Analytics Workspace
- Microsoft Defender for Cloud
- Azure Migrate
- Azure SQL Database
- Azure App Services
- Azure Database Migration Services
- Microsoft Sentinel
