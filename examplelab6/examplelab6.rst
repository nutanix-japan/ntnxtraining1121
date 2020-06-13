.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_6:

-------------
Distributed Storage Fabric
-------------

Creating a Container with Compression Enabled
+++++++++++++++++++++++++++++++++++++++++++++++

In this exercise you will create a new storage container with compression enabled.

1.	Log on to the **Prism** interface, if needed, and switch to the Storage dashboard.
2.	On the **Storage** dashboard **Overview** page, examine the **Capacity Optimization** widget at the lower left. It will either show **There are no Capacity Optimization savings to show** or minimal optimization savings. This is because neither compression, deduplication, nor erasure coding has been enabled on any storage containers. Minimal savings may appear for the VMs created earlier, due to having thin provisioned disks.

.. figure:: images/1.png
 
3.	In the upper-right corner of the browser window, click **+ Storage Container**.
4.	In the **Create Storage Container** window, type: **Compressed-Container** in the **Name** field.

.. figure:: images/2.png
 
5.	Click **Advanced Settings**.
6.	Click the **Compression** check box and ensure that the **Delay in Minutes** field is set to **0**. This will enable compression on write.

.. figure:: images/3.png
 
7.	Click **Save**.

Creating a Container without Compression
+++++++++++++++++++++++++++++++++++++++++++++++

In this exercise you will create a new storage container without compression.

1.	In the upper right corner of the browser window, click **+ Storage Container**.

2.	In the **Create Storage Container** window, type: **NotCompressed-Container** in the Name field.

3.	Click **Save**.
	
.. Note::  
   Do not change anything within advanced settings. 
 
Comparing Data in a Compressed vs Uncompressed Container
+++++++++++++++++++++++++++++++++++++++++++++++

In this exercise you will work individually to clone your original Windows VM and add two virtual disks. One of these virtual disks will be placed in the compressed container and the other into the uncompressed container you created in the previous exercises. Data will be generated on both virtual disks to compare results.

This exercise is composed of the following tasks:

 * Cloning a VM and add Two Virtual Disks
 * Formatting the New Virtual Disks
 * Writing a Large File to Each New Virtual Disk
 * Observing the Result of Compression Savings

Task 1: Adding Two Virtual Disks to a Virtual Machine
.......................................................
 
In this task you will clone a Windows VM and add two virtual disks. One virtual disk will be placed in the **Compressed-Container** and the other into the **NotCompressed-Container**.

1.	From the **VM** dashboard, **Table** view, clone **Windows 2012 VM** VM.
a.	Select the VM and click the **Clone** link. 
b.	Change the name of the clone to **DSF-<your initials>** and click Save. 
2.	Power on the new VM.
3.	Dynamically add a new disk. Select the new VM and click the **Update** link from the option below the virtual machine table and scroll down to the **Disks** section.
4.	Click **+ Add New Disk**.
5.	Use the following table to complete the **Add Disk** dialog box:
Type: **Disk**
Operation: **Allocate on Storage Container**
Bus Type: **SCSI**
Storage Container: **Compressed-Container**
Size (GiB): **10**
Index: **Next Available**
6.	Click **Add**.

.. figure:: images/4.png
 
7.	Repeat the previous steps to add a second **10GB** virtual disk to the virtual machine with the second virtual disk placed into the **NotCompressed-Container**.
8.	Click **Save**.
9.	Scroll down (if required) in the **VM** dashboard and at the lower left, under **VM DETAILS**, verify the VM is utilizing three containers:
 
 * Default-container-####
 * Compressed-Container
 * NotCompressed-Container

 Task 2: Formatting the New Virtual Disks 
.........................................

In this task you will format the newly added virtual disks in your Windows virtual machine so that you can write a large file to each of the new virtual disks.

1.	Select your **DSF-<your initials>** VM and click **Launch Console**.

2.	In the upper right corner of the virtual machine console window, click the **Ctl-Alt-Del** icon to log on to your virtual machine as **Administrator** with the password **(See Cluster Configuration Guide)**.

3.	Start the Windows Server Manager by clicking the **toolbox** icon immediately to the right of the **Windows Start** button (four pane glass). Click **File and Storage Services** in the left panel.

.. figure:: images/5.png
 
4.	Click **Disks**.

.. figure:: images/6.png
 
5.	Right-click one of the **10GB** disks and select **Bring Online**.

.. figure:: images/7.png
 
6.	Click **Yes** in the **Bring Disk Online** warning window.

7.	Repeat the previous steps to bring the second **10GB** disk online. 8.	Right-click the first **10GB** disk and select **New Volume**…

.. figure:: images/8.png
 
8.	Complete the **New Volume** wizard as follows:

a.	In **Before You begin**, click **Next**.

b.	In **Select the server and disk**, click **Next**.

c.	In the **Offline or Uninitialized Disk** warning window, click OK.

d.	In **Specify the size of the volume**, click Next.

e.	In **Assign to a drive letter or folder**, note the assigned drive letter (you will need this later) and click **Next**.

f.	In **Select File System Settings**, click **Next**.

g.	In **Confirm selections**, click **Create**.

h.	When the new volume creation has completed, click **Close**.

9.	Repeat the above steps for the second 10GB disk (again noting its assigned drive letter). When you are finished, both 10GB disks should have their status **Online** and have **GPT** partitions. 

.. figure:: images/9.png
 
10.	Close the **Server Manager** window.

Task 3: Writing a Large File to Each New Virtual Disk
....................................................... 

In this task you will write a large file to each of the new disks using the (DOS)utility **fsutil**.

1.	Go to the **VM** dashboard and click **Launch Console** of your **DSF-<your initials>** VM.

2.	Login to the Windows Desktop with the same password is initially created by the base Windows. Go to the **magnify glass** found at the bottom left of the window and type **cmd**.

3.	Run the following command:

 .. code-block:: bash
    
     Fsutil file createnew <file> <size in bytes>

For example, this command will create a 5GB file called 5gb.test in c drive:

  .. code-block:: bash
   
     Fsutil file create c:\temp\5gb.test 5368709120 

You are to substitute the drive letter of the virtual disk which you have created earlier.

4.	Repeat the command to create a large file on the second virtual disk drive you added to your virtual machine.

5.	Close the **Command Prompt** window.

6.	In **Windows File Explorer** examine the size of the two disks you added to your virtual machine along with the amount of free space on each drive. You should notice Windows is showing that approximately **5GB** of space is used on each virtual disk indicating the Windows virtual machine is completely unaware of any compression happening in the Nutanix Distributed Storage Fabric on the back end.
 
.. figure:: images/10.png

7.	Close the **VM console** window.

Task 4: Observing the Result of Compression Savings
.................................................... 

In this task you will observe the result of container compression.

1.	Switch to the **Storage** dashboard and click the **Overview** tab.

2.	Examine the **Capacity Optimization** widget in the lower left corner of the UI.

 * Do you see any immediate savings reported?
	
 .. Note::
    The savings display can take up to a few hours to display. If you do not see an immediate result, come back to this dashboard later to verify the savings due to compression.

3.	Click **Table**, then select **Storage Container**.

4.	For the **Compressed-Container** and the **NotCompressed-Container**, look in the **Used** column and compare the amount of physical space used.
 * Do you see a difference?

The **Compressed-Container** should be using significantly less space than the **NotCompressed-Container**.

.. figure:: images/11.png
 
5.	Click to select the **Compressed-Container**.
6.	Below the table of containers, on the left of the browser window, examine the values below the **Summary > Compressed-Container** box and answer the following questions:
 
 * Is compression turned on?
 * How much space has been saved due to compression?
 	
 .. Note::
 
    You may have to wait a few hours for a value to appear in this field.

 * What is the current Data Reduction Ratio?
 * What is the difference between the Compressed-Container and the NotCompressedContainer for the Data Reduction Ratio? 

7.	From the **VM** dashboard, remove the **DSF-<your initials>** VM by selecting the VM from the list and clicking Delete. Check the box to **delete** all snapshots.
 
