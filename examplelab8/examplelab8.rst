
.. _volumes_deploy:

-----------------------
Volumes
-----------------------

Overview
++++++++

.. note::

  Estimated time to complete: **30 Minutes**

The Nutanix Volumes feature (previously know as Acropolis Volumes) exposes back-end DSF storage to external consumers (guest OS, physical hosts, containers, etc.) via iSCSI.

This allows any operating system to access DSF and leverage its storage capabilities.  In this deployment scenario, the OS is talking directly to Nutanix bypassing any hypervisor.

Core use-cases for Acropolis Volumes:

- Shared Disks
- Oracle RAC, Microsoft Failover Clustering, etc.
- Disks as first-class entities
- Where execution contexts are ephemeral and data is critical
- Containers, OpenStack, etc.
- Guest-initiated iSCSI
- Bare-metal consumers
- Exchange on vSphere (for Microsoft Support)

Lab Setup
+++++++++

This lab requires Cent OS VM already provisioned on your cluster.

Configure Acropolis Block Services
++++++++++++++++++++++++++++++++++++++++++++

#.  Open ``https://*<POCxx-ABC Cluster IP>*:9440`` (https://10.42.xx.37:9440) in your browser and log in with the following credentials:

    - **Username** - admin
    - **Password** - *your cluster password*

#.  Click the Cluster name in the upper left hand corner to access the Cluster details

#.  Enter the Cluster External Data Services IP Address (10.42.xx.38) in your Assigned Cluster details

#.  Close Cluster Details and proceed to Configure Guests

    .. figure:: images/1.png


Enable and Configure ABS in Prism for Linux
++++++++++++++++++++++++++++++++++++++++++++

Ensure that the CentOS VM has access to the Network:
Login to Prism, navigate to the VM Dashboard, Table View, select the CentOS VM, and click Update, ensure that the VM has a NIC added, if it does not, add one now and attach it to VLAN0. Save the VM Settings and continue to the next steps.

Login to the Linux guest VM to get the iSCSI iqn name:

#.  Login to CentOS VM on your assigned cluster with

    - Username - root
    - Password - nutanix/4u

#.  Install ISCSI Tools: If not already installed, run the following command:

    .. code-block:: bash

      yum –y install iscsi-initiator-utils

#.  Install lsscsi tools: If not already installed, run the following command:

    .. code-block:: bash

     yum –y install lsscsi

#.  To find the iqn name run

    .. code-block:: bash

     cat /etc/iscsi/initiatorname.iscsi

#.  Copy down the iqn name of the iSCSI client initiator

    Example:

    .. figure:: images/10.png


Create a Volume Group in Prism:
++++++++++++++++++++++++++++++++++++++++++++

#.  Login to Prism

#.  Navigate to the Storage Dashboard

#.  Click **+ Volume Group** to create a new Volume Group

#.  In the Volume Group Window give the volume group a name ``mylinuxvg``

#.  Add a new disk and select default container, input a size for the disk of 60 and click **Add**

#.  In the **Client** section , click "Add New client", enter the iqn name of the Linux iSCSI initiator you copied down in step 5 of the previous section and click **Add**.

#.  Then click **Save**

Connect ABS disks to Linux VM:
..............................

#.  Discover the Nutanix ABS target by running the command

#.  Find the <DataServicesIP> from Prism Dashboard by clicking on the cluster name (PHX-POC-xxx) on the top left hand corner and use it in the following command. 

    .. code-block:: bash
      
      iscsiadm -m discovery -t sendtargets -p <DataServicesIP>

      #It should come back with the iqn name of the Nutanix ABS target volume.  Make note of this name.

    Example:

    .. figure:: images/11.png

#.  Run the following command to verify you only see one Nutanix vDisk on ``/dev/``

    .. code-block:: bash

      lsscsi

    .. figure:: images/12.png

#.  Now login to the ABS iSCSI LUN with the target iqn you copied from the Step 1 just above.

    .. code-block:: bash

      iscsiadm  --mode node --targetname <Nutanix.iqn.name.from.step.above> --portal <DataServicesIP> --login

    .. figure:: images/13.png

#.  Check the status session of the target by running

    .. code-block:: bash

      iscsiadm --mode session --op show

#.  Run the following command again to verify you now see the new Nutanix vDisk on ``/dev/sdb``

    .. code-block:: bash

      lsscsi

    .. figure:: images/14.png

Takeaways
++++++++++

- Nutanix allows creationg of volume groups(VG) to be presented to external servers
- Nutanix VG are highly avaialble behind a virtual Data Services IP in case of node failures
- Nutanix VG can be used to provide storage to external applications like Kubernetes as a Storage CSI
- Most Nutanix products (Files and Objects) use VG to store data in a performant and higly available fashion