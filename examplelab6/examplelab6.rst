.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_6:

--------------------------
Distributed Storage Fabric
---------------------------------------

Storage Operations
++++++++++++++++++++++++++++++++++

Creating a Container with Compression Enabled
................................................

In this exercise you will create a new storage container with compression enabled.

#. Log on to the **Prism** interface, if needed, and switch to the Storage dashboard.
#. On the **Storage** dashboard **Overview** page, examine the **Capacity Optimization** widget at the lower left. It will either show **There are no Capacity Optimization savings to show** or minimal optimization savings. This is because neither compression, deduplication, nor erasure coding has been enabled on any storage containers. Minimal savings may appear for the VMs created earlier, due to having thin provisioned disks.

   .. figure:: images/1.png

#. In the upper-right corner of the browser window, click **+ Storage Container**.
#. In the **Create Storage Container** window, type: **<your initials>-Compressed-Container** in the **Name** field.

   .. figure:: images/2.png

#. Click **Advanced Settings**.
#. Click the **Compression** check box and ensure that the **Delay in Minutes** field is set to **0**. This will enable compression on write.

   .. figure:: images/3.png

#. Click **Save**.

Creating a Container without Compression
................................................

In this exercise you will create a new storage container without compression.

#. In the upper right corner of the browser window, click **+ Storage Container**.

#. In the **Create Storage Container** window, type: **<your initials>-NotCompressed-Container** in the Name field.

#. Click **Save**.

   .. note::
    Do not change anything within advanced settings.

Comparing Data in a Compressed vs Uncompressed Container
................................................................................................

In this exercise you will work individually to clone your original Windows VM and add two virtual disks. One of these virtual disks will be placed in the compressed container and the other into the uncompressed container you created in the previous exercises. Data will be generated on both virtual disks to compare results.

This exercise is composed of the following tasks:

* Cloning a VM and add Two Virtual Disks
* Formatting the New Virtual Disks
* Writing a Large File to Each New Virtual Disk
* Observing the Result of Compression Savings

Adding Two Virtual Disks to a Virtual Machine
................................................

In this task you will clone a Windows VM and add two virtual disks. One virtual disk will be placed in the **<your initials>-Compressed-Container** and the other into the **<your initials>-NotCompressed-Container**.

#. From the **VM** dashboard, **Table** view, clone **Windows 2012 VM** VM.
#. Select the VM and click the **Clone** link.
#. Change the name of the clone to **DSF-<your initials>** and click Save.
#. Power on the new VM.
#. Dynamically add a new disk. Select the new VM and click the **Update** link from the option below the virtual machine table and scroll down to the **Disks** section.
#. Click **+ Add New Disk**.
#. Use the following table to complete the **Add Disk** dialog box:

   Type: **Disk**
   Operation: **Allocate on Storage Container**
   Bus Type: **SCSI**
   Storage Container: **<your initials>-Compressed-Container**
   Size (GiB): **10**
   Index: **Next Available**

#. Click **Add**.

   .. figure:: images/4.png

#. Repeat the previous steps to add a second **10GB** virtual disk to the virtual machine with the second virtual disk placed into the **<your initials>-NotCompressed-Container**.
#. Click **Save**.
#. Scroll down (if required) in the **VM** dashboard and at the lower left, under **VM DETAILS**, verify the VM is utilizing three containers:

   * Default-container-####
   * Compressed-Container
   * NotCompressed-Container

Formatting the New Virtual Disks
................................................

In this task you will format the newly added virtual disks in your Windows virtual machine so that you can write a large file to each of the new virtual disks.

#. Select your **DSF-<your initials>** VM and click **Launch Console**.

#. In the upper right corner of the virtual machine console window, click the **Ctl-Alt-Del** icon to log on to your virtual machine as **Administrator** with the password **(See Cluster Configuration Guide)**.

#. Start the Windows Server Manager by clicking the **toolbox** icon immediately to the right of the **Windows Start** button (four pane glass). Click **File and Storage Services** in the left panel.

   .. figure:: images/5.png

#. Click **Disks**.

   .. figure:: images/6.png

#. Right-click one of the **10GB** disks and select **Bring Online**.

   .. figure:: images/7.png

#. Click **Yes** in the **Bring Disk Online** warning window.

#. Repeat the previous steps to bring the second **10GB** disk online. 8.	Right-click the first **10GB** disk and select **New Volume**…

   .. figure:: images/8.png

#. Complete the **New Volume** wizard as follows:

   a.	In **Before You begin**, click **Next**.

   b.	In **Select the server and disk**, click **Next**.

   c.	In the **Offline or Uninitialized Disk** warning window, click OK.

   d.	In **Specify the size of the volume**, click Next.

   e.	In **Assign to a drive letter or folder**, note the assigned drive letter (you will need this later) and click **Next**.

   f.	In **Select File System Settings**, click **Next**.

   g.	In **Confirm selections**, click **Create**.

   h.	When the new volume creation has completed, click **Close**.

#. Repeat the above steps for the second 10GB disk (again noting its assigned drive letter). When you are finished, both 10GB disks should have their status **Online** and have **GPT** partitions.

   .. figure:: images/9.png

#. Close the **Server Manager** window.

Writing a Large File to Each New Virtual Disk
................................................

In this task you will write a large file to each of the new disks using the (DOS)utility **fsutil**.

#. Go to the **VM** dashboard and click **Launch Console** of your **DSF-<your initials>** VM.

#. Login to the Windows Desktop with the same password is initially created by the base Windows. Go to the **magnify glass** found at the bottom left of the window and type **cmd**.

#. Run the following command:

   .. code-block:: bash

     fsutil file createnew <file> <size in bytes>

   For example, this command will create a 5GB file called 5gb.test in c drive:

   .. code-block:: bash

     fsutil file create c:\temp\5gb.test 5368709120

   You are to substitute the drive letter of the virtual disk which you have created earlier.

#. Repeat the command to create a large file on the second virtual disk drive you added to your virtual machine.

#. Close the **Command Prompt** window.

#. In **Windows File Explorer** examine the size of the two disks you added to your virtual machine along with the amount of free space on each drive. You should notice Windows is showing that approximately **5GB** of space is used on each virtual disk indicating the Windows virtual machine is completely unaware of any compression happening in the Nutanix Distributed Storage Fabric on the back end.

   .. figure:: images/10.png

#. Close the **VM console** window.

Observing the Result of Compression Savings
................................................

In this task you will observe the result of container compression.

#. Switch to the **Storage** dashboard and click the **Overview** tab.

#. Examine the **Capacity Optimization** widget in the lower left corner of the UI.

   * Do you see any immediate savings reported?

     .. note::
      The savings display can take up to a few hours to display. If you do not see an immediate result, come back to this dashboard later to verify the savings due to compression.

#. Click **Table**, then select **Storage Container**.

#. For the **<your initials>-Compressed-Container** and the **<your initials>-NotCompressed-Container**, look in the **Used** column and compare the amount of physical space used.
   * Do you see a difference?

   The **<your initials>-Compressed-Container** should be using significantly less space than the **<your initials>-NotCompressed-Container**.

   .. figure:: images/11.png

#. Click to select the **<your initials>-Compressed-Container**.
#. Below the table of containers, on the left of the browser window, examine the values below the **Summary > <your initials>-Compressed-Container** box and answer the following questions:

   * Is compression turned on?
   * How much space has been saved due to compression?

     .. note::

      You may have to wait a few hours for a value to appear in this field.

   * What is the current Data Reduction Ratio?
   * What is the difference between the Compressed-Container and the NotCompressedContainer for the Data Reduction Ratio?

#. From the **VM** dashboard, remove the **DSF-<your initials>** VM by selecting the VM from the list and clicking Delete. Check the box to **delete** all snapshots.
