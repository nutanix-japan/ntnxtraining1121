.. title:: Nutanix XMEN Bootcamp

.. toctree::
  :maxdepth: 2
  :caption: AOS Cluster Track
  :name: _labs
  :hidden:

  examplelab1/examplelab1
  examplelab2/examplelab2
  examplelab3/examplelab3
  examplelab4/examplelab4
  examplelab5/examplelab5
  examplelab6/examplelab6

.. toctree::
  :maxdepth: 2
  :caption: Cluster Resiliency and Protection
  :name: _resiliency
  :hidden:

  examplelab9/examplelab9
  examplelab10/examplelab10

.. toctree::
  :maxdepth: 2
  :caption: Cluster Management
  :name: _management
  :hidden:

  examplelab11/examplelab11
  examplelab12/examplelab12
  examplelab13/examplelab13


.. toctree::
  :maxdepth: 2
  :caption: Cluster Workload Migration
  :name: _move
  :hidden:

  examplelab7/examplelab7

.. toctree::
  :maxdepth: 2
  :caption: Nutanix Volumes
  :name: _volumes
  :hidden:

  examplelab8/examplelab8

.. toctree::
   :maxdepth: 2
   :caption: Era with MSSQL Track
   :name: _dbs
   :hidden:

   configure_mssql/configure_mssql
   admin_mssqldb/admin_mssqldb
   deploy_mssql_era/deploy_mssql_era
   webtier/webtier
   patch_sql/patch_sql

.. toctree::
  :maxdepth: 2
  :caption: Appendix
  :name: _appendix
  :hidden:

  appendix/appendix

.. _getting_started:

---------------
Getting Started
---------------


.. What's New
.. ++++++++++
..
.. - Workshop updated for the following software versions:
..     - AOS & PC 5.11
..
.. - Optional Lab Updates:
..
.. - Added :ref:`example_lab_3`

Agenda
++++++

There are two tracks participants could work on. There are no inter-dependencies. The following tracks can be done in order of preference.

AOS Track
....................

.. note::

	Estimated time to complete this track is 2 hours

- Cluster Basics
   - Nutanix Technology Overview
   - Nutanix Configuration
   - Deploying and Managing Workloads
   - Security and Compliance
- Cluster Resiliency and Protection
- Cluster Management
- Cluster Workload Migration
- Nutanix Volumes

Era with MSSQL Track
......................

.. note::

	Estimated time to complete this track is 2 hours

- Configure MSSQL
- Admin MSSQL with Era
- Deploy MSSQL with Era
- Patching MSSQL

Introductions
+++++++++++++

- Name
- Familiarity with Nutanix

Initial Setup
+++++++++++++

- Take note of the *Passwords* being used.
- Log into your virtual desktops (connection info below)

Cluster assignment
++++++++++++++++++

Your cluster assignments can be found in `Lookup <http://10.42.8.58:8090/>`_. Enter your registered email address to find your details

.. .. note::
..   If these are Single Node Clusters (SNCs) pay close attention on the networking part. The SNCs are completely different setup and configured compared to the "normal" three/four node clusters

Environment Details
+++++++++++++++++++

Nutanix Workshops are intended to be run in the Nutanix Hosted POC environment. Your cluster will be provisioned with all necessary images, networks, and VMs required to complete the exercises.

Networking
..........

As we are able to provide single node clusters in the HPOC environment, we need to describe each cluster separately. The clusters are setup and configured differently.

Single Node HPOC clusters
-----------------------------

Hosted Single Node POC clusters follow a standard naming convention:

- **Cluster Name** - SPOC\ *XYZ*
- **Subnet** - 10.\ **38**\ .\ *XYZ*\ .0
- **Cluster IP** - 10.\ **38**\ .\ *XYZ*\ .37

For example:

- **Cluster Name** - SPOC010
- **Subnet** - 10.38.10.0
- **Cluster IP** - 10.38.10.37 for the VIP of the Cluster


Throughout the Workshop there are multiple instances where you will need to substitute *XYZ* with the correct octet for your subnet, for example:

.. list-table::
  :widths: 25 75
  :header-rows: 1

  * - IP Address
    - Description
  * - 10.38.\ *XYZ*\ .37
    - Nutanix Cluster Virtual IP
  * - 10.38.\ *XYZ*\ .39
    - **PC** VM IP, Prism Central
  * - 10.38.\ *XYZ*\ .41
    - **DC** VM IP, NTNXLAB.local Domain Controller

Each cluster is configured with 1 VLANs which can be used for User VMs:

.. list-table::
  :widths: 25 25 10 40
  :header-rows: 1

  * - Network Name
    - Address
    - VLAN
    - DHCP Scope
  * - Primary
    - 10.38.\ *XYZ*\ .1/26
    - 0
    - 10.38.\ *XYZ*\ .50-10.21.\ *XYZ*\ .124
  .. * - Secondary
  ..   - 10.38.\ *XYZ*\ .129/25
  ..   - *XYZ1*
  ..   - 10.38.\ *XYZ*\ .132-10.21.\ *XYZ*\ .253

.. Single Node HPOC Clusters
.. -------------------------
..
.. For some workshops we are using Single Node Clusters (SNC). The reason for this is to allow more people to have a dedicated cluster but still have enough free clusters for the bigger workshops including those for customers.
..
.. The network in the SNC config is using a /26 network. This splits the network address into four equal sizes that can be used for workshops. The below table describes the setup of the network in the four partitions. It provides essential information for the workshop with respect to the IP addresses and the services running at that IP address.
..
.. .. list-table::
..   :widths: 15 15 15 15 40
..   :header-rows: 1
..
..   * - Partition 1
..     - Partition 2
..     - Partition 3
..     - Partition 4
..     - Service
..     - Comment
..   * - 10.42.x.1
..     - 10.42.x.65
..     - 10.42.x.129
..     - 10.42.x.193
..     - Gateway
..     -
..   * - 10.42.x.5
..     - 10.42.x.69
..     - 10.42.x.133
..     - 10.42.x.197
..     - AHV Host
..     -
..   * - 10.42.x.6
..     - 10.42.x.70
..     - 10.42.x.134
..     - 10.42.x.198
..     - CVM IP
..     -
..   * - 10.42.x.7
..     - 10.42.x.71
..     - 10.42.x.135
..     - 10.42.x.199
..     - Cluster IP
..     -
..   * - 10.42.x.8
..     - 10.42.x.72
..     - 10.42.x.136
..     - 10.42.x.200
..     - Data Services IP
..     -
..   * - 10.42.x.9
..     - 10.42.x.73
..     - 10.42.x.137
..     - 10.42.x.201
..     - Prism Central IP
..     -
..   * - 10.42.x.11
..     - 10.42.x.75
..     - 10.42.x.139
..     - 10.42.x.203
..     - AutoDC IP(DC)
..     -
..   * - 10.42.x.32-37
..     - 10.42.x.96-101
..     - 10.42.x.160-165
..     - 10.42.x.224-229
..     - Objects 1
..     -
..   * - 10.42.x.38-58
..     - 10.42.x.102-122
..     - 10.42.x.166-186
..     - 10.42.x.230-250
..     - Primary network IPAM
..     - 6 Free IPs free for static assignment
..

Credentials
...........

.. note::

  The *<Cluster Password>* is unique to each cluster and will be provided by the leader of the Workshop.

.. list-table::
   :widths: 25 35 40
   :header-rows: 1

   * - Credential
     - Username
     - Password
   * - Prism Element
     - admin
     - *<Cluster Password>*
   * - Prism Central
     - admin
     - *<Cluster Password>*
   * - Controller VM
     - nutanix
     - *<Cluster Password>*
   * - Prism Central VM
     - nutanix
     - *<Cluster Password>*

.. Each cluster has a dedicated domain controller VM, **DC**, responsible for providing AD services for the **NTNXLAB.local** domain. The domain is populated with the following Users and Groups:
..
.. .. list-table::
..    :widths: 25 35 40
..    :header-rows: 1
..
..    * - Group
..      - Username(s)
..      - Password
..    * - Administrators
..      - Administrator
..      - nutanix/4u
..    * - SSP Admins
..      - adminuser01-adminuser25
..      - nutanix/4u
..    * - SSP Developers
..      - devuser01-devuser25
..      - nutanix/4u
..    * - SSP Consumers
..      - consumer01-consumer25
..      - nutanix/4u
..    * - SSP Operators
..      - operator01-operator25
..      - nutanix/4u
..    * - SSP Custom
..      - custom01-custom25
..      - nutanix/4u
..    * - Bootcamp Users
..      - user01-user25
..      - nutanix/4u

Access Instructions
+++++++++++++++++++

The Nutanix Hosted POC environment can be accessed a number of different ways:

Lab Access User Credentials
...........................

PHX Based Clusters:
**Username:** PHX-SPOCxxx-User01 (up to PHX-SPOCxxx-User5), **Password:** *<Provided by Instructor>*


Frame VDI
.........

Login to: https://console.nutanix.com/x/labs

.. **Nutanix Employees** - Use your **NUTANIXDC** credentials

Go to HPOC `Lookup <http://10.42.8.58:8090/>`_ here to get your login credentials for Frame user, and cluster details.

**Non-Employees** - Use **Lab Access User** Credentials

.. Parallels VDI
.. .................
..
.. PHX Based Clusters Login to: https://xld-uswest1.nutanix.com
..
.. RTP Based Clusters Login to: https://xld-useast1.nutanix.com
..
.. **Nutanix Employees** - Use your **NUTANIXDC** credentials
.. **Non-Employees** - Use **Lab Access User** Credentials

Pulse Secure VPN
..........................

Download the client:

PHX Based Clusters Login to: https://xld-uswest1.nutanix.com

Install the client.

In Pulse Secure Client, **Add** a connection:

For PHX:

- **Type** - Policy Secure (UAC) or Connection Server
- **Name** - X-Labs - PHX
- **Server URL** - xlv-uswest1.nutanix.com

Go to HPOC `Lookup <http://10.42.8.58:8090/>`_ here to get your login credentials for Frame user, and cluster details.

Login to VPN to access your HPOC environment to do the labs.

.. For RTP:
..
.. - **Type** - Policy Secure (UAC) or Connection Server
.. - **Name** - X-Labs - RTP
.. - **Server URL** - xlv-useast1.nutanix.com
