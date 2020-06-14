.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_8:

-------------
Acropolis Block Service
-------------

Deploying a Windows VM
++++++++++++++++

In this exercise you will deploy a **Windows 2012 R2** VM and create virtual machines for **iSCSI** configurations.

1.  From the Prism VM dashboard, select **+ Create VM**. Fill out the following:

  Name: **<your_initials>-iscci-Win**

  VCPU(s): **1**

  Number of Cores Per VCPU: **2**

  Memory: **4**

2.  Scroll down to the Disks section and Select **+ Add New Disk**. 
  
  Type: **Disk**

  Operation: **Clone from Image Service**

  Bus Type: Leave at default

  Image: **Windows 2012**

   a. Click **Add**.

   b. Scroll down to the **Network Adapters (NIC)** section.

3.  Select **+ Add New NIC**.

   a. Select network **Unmanaged Client Network**.

   b. Click **Add**.

4.  Click **Save** in the **Create VM** dialogue window. 

5.  When the virtual machine has been created, click **Power On** to start the virtual machine.

Creating a Volume Group for Windows
+++++++++++++++++++++++++++++++++++

In this exercise you will create a volume group in your cluster for your Windows VM. This volume group will contain the iSCSI targets that will be accessed by the Windows iSCSI client (initiator). The iSCSI initiator controls all command and data traffic within an iSCSI configuration.

1.  If you are not logged into your Prism UI, log on as the **admin** user.

2.  In the upper-left corner of the browser window, click on your cluster name.

.. figure:: images/1.png
 
3.  In the **Cluster Details** window, in the **iSCSI DATA SERVICES IP** text box, enter the **Cluster Data Services IP** from **Cluster Configuration Guide**.

.. figure:: images/2.png
 
4.  Click **Save**.

5.  Switch to the **Storage** dashboard.

6.  In the upper-right corner of the browser window, click **+ Volume Group**.

7.  In the **Create Volume Group** window, in the **Name** text box enter the name **<your initials>Win-VG**.

.. figure:: images/3.png
 
8.  In the Create Volume Group window, click **+ Add New Disk**.

9.  In the **Add Disk** window, fill out the fields as follows:
Storage Container: **default-container-#####**
Sizer(GiB): 10
 
.. figure:: images/4.png

10. Click **Add**.

11. Repeat the previous steps one more time to have a total of two disks in the volume group.
  
 .. Note::
   Make sure you select the default-container-##### each time you add a disk to the Volume Group, it will not be selected by default.

12. When you are done, the **Create Volume Group** window should have two 10GB disks listed under **Storage**.
 
.. figure:: images/5.png

13. Click **Save**.

Configuring the Windows VM as an iSCSI Initiator
++++++++++++++++++++++++++++

In this exercise you will configure a **Windows 2012 VM** as an iSCSI initiator. The iSCSI initiator, also known as the iSCSI Client, controls all command and data traffic within an iSCSI configuration.

1.  Switch to the **VM** dashboard and click the **Table** tab.

2.  Click to select the **<your initials>-iscsi-Win** VM.

3.  Click **Launch Console**.

4.  Log on to the Windows VM as **Administrator** .(if you are asked to create a new password for the windows please refer to Cluster Configuration Guide for the information)

5.  Click the **four panel Windows** icon in the task bar and click the **magnifying glass** at the upper right.

6.  In the **search** field type **cmd** and click **Command Prompt** to open a **Command Prompt** window.

7.  In the **Command Prompt** window enter the following command:

 .. code-block:: bash
    
    services.msc

8.  Scroll down in the **Services** window, right-click **Microsoft iSCSI Initiator Service**, and select **Properties**.
9.  In the **Properties** window, click the **Startup type** drop down menu and select **Automatic**.

.. figure:: images/6.png
 
10. Under **Service Status**, click **Start**.

11. Click **OK** and close the **Services** window.

12. In the **Command Prompt** window enter the following command:

 .. code-block:: bash
    
    firewall.cpl

13. In the upper-left corner of the **Windows Firewall** window, click **Allow an app or feature through Windows Firewall**.

.. figure:: images/7.png
 
14. In the **Allowed Apps** window, under **Allowed apps and features**, scroll down and check the check box to the left of **iSCSI Service**. Check the check box under the **Public** column also.

.. figure:: images/8.png
 
15. Click **OK** and close the **Windows Firewall** window.

16. In the **Command Prompt** window enter the following command:

 .. code-block:: bash

    iscsicpl.exe

17. Click the **Configuration** tab at the top (right).

18. Click **Change**…

19. Enter the following into the **Initiator Name** text box:

 .. code-block:: bash

   iqn.1991-05.com.microsoft:win-1
  
 .. Note ::

   You should only have to backspace over the last few characters in the existing name and replace them with the digit 1.

.. figure:: images/9.png
 
20. Click **OK**.

21. Click **OK** to exit the iSCSI configuration utility. 

Configuring a Windows VM for Access to a Volume Group
++++++++++++++++++++++++++++++++++++++++++++++++++++

In this exercise you will configure your **Windows 2012** virtual machine to discover and access the two virtual disks (targets) in the volume group that you created previously in this lab.

1.  From the Prism UI, go to the **Storage** dashboard -> **Table -> Volume Group tab**.

2.  Select the **<your initials>-Win-VG** volume group and click the **Update** link below the **Volume Group** table.

3.  In the **Update Volume Group** dialog box, scroll down and click **+ Add New Client**.

4.  In the **Add iSCSI Client** dialog box, enter the following into the Client IQN/IP Address text box: **iqn.1991-05.com.microsoft:win-1**

5.  Double check your entry for typos and click **Add**.

6.  Click **Save**.

7.  Verify the Client IQN in the **VOLUME GROUP DETAILS** panel at the lower left.

.. figure:: images/10.png
 
8.  Return to the console of your **<your initials>-iscsi-Win VM**.

9.  In the **Command Prompt** window, enter the following command:

 .. code-block:: bash
    
    iscsicpl.exe

10. Click the **Discovery** tab at the top.

11. Click **Discover Portal…**

.. figure:: images/11.png
 
12. In the **Discover Target Portal** window, enter your cluster’s external data services IP address into the **IP address or DNS name** text box. Leave the **Port** field at its default value.
  
.. Note::
 
   Your cluster’s external data services IP address can be found on your Cluster Configuration Guide.

.. figure:: images/12.png
 
13. Click **OK**.
14. Click the **Targets** tab.
15. If you do not see the two targets from the volume group, click **Refresh**. 
  
.. Note::
 
   The targets will initially display as Inactive.

.. figure:: images/13.png 

16. Select one of the targets and click **Connect**.

17. In the **Connect To Target** dialog box, click **OK**. (if Enable multi-path is not checked, please checked the box before clicking **OK**)
 
.. figure:: images/14.png 

18. The target you just connected should show a status change from **Inactive** to **Connected**.

.. figure:: images/15.png 
 
19. Repeat with the second target.

20. Click **OK**.

21. In the **Command Prompt** window enter the following command:

 .. code-block:: bash

    diskmgmt.msc

22. Scroll down the **Disk Management** window and you should see the two targets listed. 

.. figure:: images/16.png 
 
23. For each disk, right-click the gray box where it shows **Unknown and Offline**. Select **Online**, right-click again and select **Initialize Disk**. In the initialize Disk dialog box, take the defaults and click **OK**. 
24. For each disk, right click the open field, marked **10.00GB Unallocated** and select **New Simple Volume**. In the wizard, click **Next** and take the defaults to the summary page and click **Finish**. You should see each disk mounted to a drive letter.
25. Close all the windows you have opened in this exercise.
