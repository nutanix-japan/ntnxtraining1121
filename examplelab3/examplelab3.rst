.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_3:

-------------
Networking
-------------

Review Existing Primary Client Network
+++++++++++++++++++++++++++++++++++++++

#. Log on to your cluster’s Prism UI (Element) as the **admin** user.

#. Click the **gear** icon, scroll down in **Settings** to the **Network** section and click **Network Configuration**.

#. Click **Virtual Networks** if not already selected.

#. Click on the **pen** icon on the Primary network

#. Note the following fields for the Primary Network. You can review the description on each field with the ? icon

   - Name: Primary
   - VLAN ID: < The default VLAN ID is always 0 >
   - IP address Management: ENABLED
   - IP address Pools
   - Override DHCP server

#. Click **Cancel** at the bottom of the screen to return to the Networking menu.

Creating an Unmanaged Client Network
++++++++++++++++++++++++++++++++++++

In this exercise you will create an unmanaged network.

#. Log on to your cluster’s Prism UI (Element) as the **admin** user.

#. Click the **gear** icon, scroll down in **Settings** to the **Network** section and click **Network Configuration**.

#. Click **Virtual Networks** if not already selected.

#. Click **Create Network**

#. Fill out the **Create Network** dialog box as follows:

   * Name: **<Your-Intials>-Unmanaged Client Network**

   * VLAN ID: **0**

   * Enable IP address Management: **Leave unchecked**

   .. figure:: images/3.png

#. Click **Save** to create the network.

Managing Open vSwitch (OVS)
++++++++++++++++++++++++++++++++++++

In this exercise you will explore a few commands to manage Open vSwitch (OVS) from the CVM and use those commands to build an additional virtual switch.

#. Using PuTTY, establish an SSH connection to one of your CVMs and log on with the **nutanix** user and password **(Refer to Cluster Configuration Guide)**.

#. Use **allssh** to execute commands on all CVMs. To view network interface information, type the command:

   .. code-block:: bash

     allssh manage_ovs show_interfaces

   * How many network interfaces are on each node?
   * How many network interfaces are 10GbE?
   * How many network interfaces are 1GbE?

#. To list existing bridges for each Nutanix node in the cluster, type the command:

   .. code-block:: bash

     allssh manage_ovs show_bridges

   * How many bridges are on each node?

#. To show bridge uplinks for each Nutanix node in the cluster, type the command:

   .. code-block:: bash

    allssh manage_ovs show_uplinks

   * Which network interfaces are on bond (or port) br0-up?
