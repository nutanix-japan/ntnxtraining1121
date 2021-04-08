.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_7:

----------------------------------------
Migrating Workloads with Nutanix Move
-----------------------------------------
Nutanix Move
+++++++++++++++++++++

Deploy this VM on your assigned cluster if directed to do so as part of **Lab Setup**.

.. raw:: html

  <strong><font color="red">Only deploy the VM once, it does not need to be cleaned up as part of any lab completion.</font></strong>

Installing Move VM
................................................

#. Login to you Prism Element

#. Upload an Move image using **Settings > Image Configuration**

#. Click on **Upload Image** and enter the following values:

   - **Name** Initials-MoveImage
   - **Annotation** - (optional)
   - **Image Type** - Disk
   - **Storage Container** - SelfServiceContainer
   - **URL** - http://10.42.194.11/workshop_staging/move-3.6.0.qcow2

#. Once the image is ready, proceed to create Move VM

#. In **Prism Central** > select :fa:`bars` **> Virtual Infrastructure > VMs**, and click **Create VM**.

#. Fill out the following fields:

   - **Name** - *Initials*-Move
   - **Description** - (Optional) Description for your VM.
   - **vCPU(s)** - 1
   - **Number of Cores per vCPU** - 2
   - **Memory** - 2 GiB

   - Select **+ Add New Disk**
   - **Type** - DISK
   - **Operation** - Clone from Image Service
   - **Image** - Initials-MoveImage
   - Select **Add**

   - Select **Add New NIC**
   - **VLAN Name** - Secondary
   - Select **Add**

#. Click **Save** to create the VM.

#. Power on the VM.

Verify Move VM Install
................................................

Open **Prism Element > VM**

Confirm that **Move VM** is visible and powered-on.

Setting up a Move VM
................................................
In this exercise, you will work towards deploying Nutanix Move VM on a Nutanix AHV cluster.

#. In your Prism Element UI, identify the IP address of the Move VM.
#. Open a new tab in your browser and enter the IP of your **Move** VM.
#. Select the **I have read and agreed to terms and conditions** check box and click **Continue**.

   .. figure:: images/1.png

#. Click **OK** in the **Customer Experience Program** popup window.
#. Set a new password for the **nutanix** user. Set the password as **Nutanix/4u** with the CAP letter N).
#. Log on using the new user and password.
#. In the Move Supports dialog bog, click Continue.

   .. figure:: images/2.png

#. Upgrade Move VM to latest version if there a pop-up requesting this. This should only take a few minutes. The option will popup or go to **Settings > Upgrade** to complete this step.

Configuring Move
................................................

#. The **Move** dashboard displays **Source Environments**, **Target Environments** and **Migration Plans**.
#. On the upper left side of the Move UI, click **+ Add Source**.
#. In the **Add Source Environment** dialog box, select **VMware ESXi**.

   .. figure:: images/3.png

#. Enter the following values into the respective fields:
   - Source Name: **VMWare vCenter**
   - Environment Name: **Source**
   - vCenter Server: **<vCenter IP Address> Ask your instructor**
   - vCenter Password: **Ask your instructor**

   .. figure:: images/4.png

#. Click **Add**.

#. In the new **SOURCE** box, click the **ellipse (…)** in the upper right corner and in the presented menu, choose **Refresh**. This will initiate a query to update Move with the latest changes in vCenter.

    .. figure:: images/5.png

#. In the left panel, click **+ Add Target** and enter the following values:

   - Target Name: **<your cluster name>**
   - Nutanix Environment: **<cluster external IP address> See Cluster Configuration Guide**
   - User Name: **admin**
   - Password: **Ask your instructor**

#. Click **Add**.

   .. figure:: images/6.png

#. In the new **Target <your cluster name>** card, click the **ellipsis (…)** in the upper right corner and in the presented menu choose **Refresh**. This will initiate a query to update Move with the latest changes in your Nutanix target cluster.

Configuring a Migration Plan
................................................

In this exercise, you will create a migration plan and initiate the migration.

.. note::

 In this part of the exercise, you are to create a migration plan and initiate the migration of virtual machines which are located in the ESXi SOURCE to the TARGET Cluster you are currently working on. There are already pre-created VMs mapping to your User Account name of your VDI session. The target machines you are to migrate should corresponding to you VDI User  Account name. e.g PHX-POC037-User01, PHX-POC37-User02 etc

#. Click **+ New Migration Plan** on the top right side of your screen to create a new migration plan.

#. Enter Plan Name as: Migration Plan <your initials>

   .. figure:: images/7.png

#. Click **Proceed**.

#. In the source target, select **SOURCE – VMWare vCenter** as the source of your migration.

   .. figure:: images/8.png

#. In the target, select **Target-<your cluster name>** as the destination of the migration.

#. Select **default-container-#########** as your target container and click **NEXT** to proceed.

   .. figure:: images/9.png

#. In **Select VMs** in step2 of the migration plan, please click on the + symbol beside the virtual machine of your name. On the right side of the screen, the selected source VM will appear in your screen.

   .. figure:: images/10.png

#. Click **Next** to proceed to Network Configuration.

#. Select Unmanaged Client as the Target Network and leave Test Network (optional) as default and click NEXT to proceed.

   .. figure:: images/11.png

#. In **VM Preparation** step, key in the following parameters:

   - Preparation Mode: **Automatic**
   - Credentials for Source VMs:  Under Windows VMs key in the **User Name** and **Password** (refer to Cluster Configuration Guide)
   - Override Individual VM Settings: **Leave as default**
   - TimeZone: **Leave as Default**
   - Retain MAC Addresses from the Source VMs: **Ensure box is UNCHECKED**
   - **Btpass Guest Operations on Source VMs: Ensure box is UNCHECKED**
   - Manage Settings for Individual VMs: Leave as Default
   - Schedule Data Seeding: **Ensure box is UNCHECKED**

#. Click **NEXT**.

#. Review your final settings in **Summary** page, and click **Save** and Start to proceed with the migration.

#. Under **Migration Plans** page, you will be able to monitor the migration progress:

   .. figure:: images/12.png

#. Click on **In Progress** and to see the migration in detailed.

   .. figure:: images/13.png

#. Once the status bar has hit 100%, and display the Cutover status as shown below, you are ready to perform a cut-over.

   .. figure:: images/14.png

#. Click on the **Cutover** button:

   .. figure:: images/15.png

#. And once the Migration Status shows Completed, you should be able to view the target VM.

#. Go into your Prism Element UI and you should view the newly migrated VM under the VM list.

   .. figure:: images/16.png

Congratulations! You have successfully performed a VM migration using Nutanix Move.
