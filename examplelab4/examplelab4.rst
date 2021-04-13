.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_4:

--------------------------
Virtual Machine Management
--------------------------


Creating a Windows Virtual Machine
+++++++++++++++++++++++++++++++++++

In this exercise you will create a Windows Server VM from a Windows installation ISO image.

AHV provides an **Image Service** feature allows you to build a store of imported files that you can use to create a CD-ROM from an ISO image or an operating system Disk from a disk image when creating a VM. The Image Service supports raw, vhd, vhdx, vmdk, vdi, iso, and qcow2 disk formats


This exercise is composed of the following tasks:

* Build a Windows Virtual Machine
* Install a Windows Operating System
* Attach and install Nutanix Guest Tools

.. note::

   You can explore available images and upload images under :fa:`cog` > **Image Configuration** in Prism Element

In order to provide high performance IO to VMs, AHV requires the installation of para-virtualized drivers into the guest (similar to VMware Tools). For Windows guests specifically, these drivers must be loaded during installation in order for the VM’s disk to be accessible by the Windows installer.

Nutanix validates and distributes these drivers via http://portal.nutanix.com. The ISO image containing the drivers has already been uploaded to the Image Service.

Building a Windows Virtual Machine
.............................................

#. In **Prism Element** > **VM** > **Table**, click **+ Create VM**.

#. Fill out the following fields and click **Save**:

   Leave other settings at their default values.

   * **Name** - Initials-Windows_VM
   * **Description**-(Optional) Description for your VM.
   * **vCPU(s)** - 2
   * **Number of Cores per vCPU** - 1
   * **Memory** - 4 GiB
   .. * Select next to CDROM
   ..    - **Operation** - Clone from Image Service
   ..    - **Image** – Virt IO
   ..    - Select **Update**

#. This will mount the Windows Server ISO from the Image Service for boot/installation

   * **Select** + **Add New** Disk
      - **Type** - DISK
      - **Operation** – Clone from Image Service
      - **Image** – Windows 2012
      - Select **Add**

#. This will add a disk containing the Windows boot media.

   * **Select Add New NIC**
      - VLAN Name – **<Your-Intials>-Unmanaged Client Network**
      - Select **Add**

   This will add a single virtual NIC to the VM on the selected Virtual  Network

#. Click **Save** to create the VM.

   .. note::

    At the following URL you can find the supported Operating Systems: https://portal.nutanix.com/page/documents/compatibility-matrix/guestos

#. Select the VM, then click **Power On** from the list of action links (below the table) to turn on the VM.

#. Select the VM, then click **Launch Console** from the **Actions** drop-down menu to access an HTML5 console to interact with the VM.

#. When prompted the enter the password for the Administrator, please enter password as **Nutanix/4u**

   .. figure:: images/1.png

   .. figure:: images/2.png

#. Following OS installation you can complete the Nutanix Guest Tools (NGT) installation by selecting the VM in Prism and clicking Manage Guest Tools > Enable Nutanix Guest Tools > Mount Guest Tools,and clicking Submit.

   This will use the virtual CD-ROM device to mount the NGT installation ISO to the VM. NGT includes the previously installed VirtIO drivers, as well as services to support Self-Service File Restore (SSR) and Application Consistent (VSS) snapshots.

   .. figure:: images/3.png

#. Return to the VM console to complete the NGT installation by clicking on the Nutanix Guest Tools CD and follow through the installation wizard.

   .. figure:: images/4.png

Congrats! You have successfully deployed a Windows VM!

Creating a Linux Virtual Machine
+++++++++++++++++++++++++++++++++++

In this exercise you will create a CentOS VM from an existing, pre-installed disk image in the Image Service. It is common in many environments to have “template” style images of pre-installed operating systems. Similar to the previous exercise, the disk image has already been uploaded to the Image Service.

#. In **Prism Element** > **VM** > **Table**, click **+ Create VM**.

#. Fill out the following field and click **Save**:

   * **Name** - CentOS-<your initials>
   * **Description** - (Optional) Description for your VM.
   * vCPU(s) - 2
   * **Number of Cores per vCPU** - 1
   * **Memory** - 4 GiB
   * Select **+ Add New Disk**

     - **Type** – Disk
     - **Operation** - Clone from Image Service
     - **Image** – CentOS
     - Select **Add**
     - Boot Configuration
     - Leave the default selected **Legacy Boot**

   * Select **Add New NIC**

     - **VLAN Name** - Primary
     - Select **Add**

#. Click **Save** to create the VM.

#. Launch the console to see the VM being started.

#. Login with root and the credentials provided in the Cluster General Information site.

#. Shutdown CentOS by typing the following:

   .. code-block:: bash

     init 0

#. Close the **VM console** window.
  

Updating CPU and Memory
........................

**Individual Exercise**

In this task, you will add a CPU and increase the amount of Memory on your Windows VM.

#. From the Prism **VM** dashboard, click to select the **Windows-<your initials>** VM and in the links below the **VM** table, click **Update**.

#. In the **Update VM** dialog box, under **Compute Details**, increase the VCPU(S) from **2** to **4** and the Memory from **4** to **8**.

#. Click **Save**.

#. This should result in an update error. Dynamic bulk updates to a VM are not allowed.

   .. figure:: images/5.png


#. Modify one component at a time. Click **Update** once again for your **Windows-<your initials>** VM and in the **Update VM** dialog box, under **Computer Details**, increase the VCPU(S) from **2** to **4**.

#. Click **Save**.

#. Observe the change in the VM Dashboard for your VM. The Core column will change from **2** to **4** (two VCPUs with two cores each).

   . Repeat the update process and change the Memory from **4** to **8**.
 
