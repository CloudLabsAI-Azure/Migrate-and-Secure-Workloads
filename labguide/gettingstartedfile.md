# Getting Started with Lab

1. Once the environment is provisioned, a virtual machine (JumpVM) and lab guide will get loaded in your browser. Use this virtual machine throughout the workshop to perform the lab. You can see the number on the bottom of lab guide to switch to different exercises of the lab guide.

   ![](Images/gs-step1.png "Lab Environment")

1. To get the lab environment details, you can select the **Environment Details** tab. Additionally, the credentials will also be emailed to your registered email address. Also, you can start, stop, and restart virtual machines from the **Resources** tab.

   ![](Images/env-step2-env-details.png "Lab Environment")
 
    > You will see DeplymentID value on **Environment Details** tab, use it wherever you see SUFFIX or DeploymentID in lab steps.

1. You can validate each task by navigating to **Lab Validation** tab and clicking on **Validate** button. Please make sure you run the validation steps for each task after performing it. 

   ![](Images/upd-validation.png "Lab Environment")

## Login to Azure Portal
1. In the JumpVM, click on Azure portal shortcut of Microsoft Edge browser which is created on desktop.

     ![](Images/gs-step4-azure-portal-shortcut.png "Lab Environment")
   
1. On **Sign into Microsoft Azure** tab you will see login screen, in that enter following email/username and then click on **Next**. 
   * Email/Username: <inject key="AzureAdUserEmail"></inject>
   
     ![](Images/image7.png "Enter Email")

     > **Note:** If you get a **Download Microsoft Edge mobile app** popup, then click on **Do not show** dropdown and select **Don't show this recommendation again**. 
     
1. Now enter the following password and click on **Sign in**.
   * Password: <inject key="AzureAdUserPassword"></inject>
   
     ![](Images/image8.png "Enter Password")
     
   > If you are presented with **Help us protect your account** dialog box, then select **Skip for now** option.

      ![](Images/MFA.png "Enter Password")

   > If you are presented with **Action Required** dialog box, then select **Ask later** option.

      ![](Images/gs-step3-azure-login.png "Enter Password")
  
1. If you see the pop-up **Stay Signed in?**, click No

1. If you see the pop-up **You have free Azure Advisor recommendations!**, close the window to continue the lab.

1. If a **Welcome to Microsoft Azure** popup window appears, click **Maybe Later** to skip the tour.
   
1. Now you will see Azure Portal Dashboard, click on **Resource groups** from the Navigate panel to see the resource groups.

     ![](Images/select-rg.png "Resource groups")
   
1. Confirm you have all resource group are present as shown below.

     ![](Images/upimage10.png "Resource groups")
   
1. Now, click on the **Next** from lower right corner to move on next page.
