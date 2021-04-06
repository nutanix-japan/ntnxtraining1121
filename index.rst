.. title:: Nutanix NCP Bootcamp

.. toctree::
  :maxdepth: 2
  :caption: Cluster Basics
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

- Cluster Basics
   - Nutanix Technology Overview
   - Nutanix Configuration
   - Deploying and Managing Workloads
   - Security and Compliance
- Cluster Resiliency and Protection
- Cluster Management
- Cluster Workload Migration
- Nutanix Volumes

Introductions
+++++++++++++

- Name
- Familiarity with Nutanix

Initial Setup
+++++++++++++

- Take note of the *Passwords* being used.
- Log into your virtual desktops (connection info below)

Environment Details
+++++++++++++++++++

Nutanix Workshops are intended to be run in the Nutanix Hosted POC environment. Your cluster will be provisioned with all necessary images, networks, and VMs required to complete the exercises.

Networking
..........

Hosted POC clusters follow a standard naming convention:

- **Cluster Name** - POC\ *XYZ*
- **Subnet** - 10.**42**.\ *XYZ*\ .0
- **Cluster IP** - 10.**42**.\ *XYZ*\ .37

Throughout the Workshop there are multiple instances where you will need to substitute *XYZ* with the correct octet for your subnet, for example:

.. list-table::
   :widths: 25 75
   :header-rows: 1
   * - IP Address
     - Description
   * - 10.42.\ *XYZ*\ .37
     - Nutanix Cluster Virtual IP
   * - 10.42.\ *XYZ*\ .39
     - **PE** Data Services IP
   * - 10.42.\ *XYZ*\ .39
     - **PC** VM IP, Prism Central
   * - 10.42.\ *XYZ*\ .41
     - **DC** VM IP, NTNXLAB.local Domain Controller

Each cluster is configured with 2 VLANs which can be used for VMs:

.. list-table::
  :widths: 25 25 10 40
  :header-rows: 1
  * - Network Name
    - Address
    - VLAN
    - DHCP Scope
  * - Primary
    - 10.42.\ *XYZ*\ .1/25
    - 0
    - 10.42.\ *XYZ*\ .50-10.21.\ *XYZ*\ .124
  * - Secondary
    - 10.42.\ *XYZ*\ .129/25
    - *XYZ1*
    - 10.42.\ *XYZ*\ .132-10.21.\ *XYZ*\ .253

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

Each cluster has a dedicated domain controller VM, **DC**, responsible for providing AD services for the **NTNXLAB.local** domain. The domain is populated with the following Users and Groups:

.. list-table::
   :widths: 25 35 40
   :header-rows: 1
   * - Group
     - Username(s)
     - Password
   * - Administrators
     - Administrator
     - nutanix/4u
   * - SSP Admins
     - adminuser01-adminuser25
     - nutanix/4u
   * - SSP Developers
     - devuser01-devuser25
     - nutanix/4u
   * - SSP Consumers
     - consumer01-consumer25
     - nutanix/4u
   * - SSP Operators
     - operator01-operator25
     - nutanix/4u
   * - SSP Custom
     - custom01-custom25
     - nutanix/4u
   * - Bootcamp Users
     - user01-user25
     - nutanix/4u

Access Instructions
+++++++++++++++++++

The Nutanix Hosted POC environment can be accessed a number of different ways:

Lab Access User Credentials
...........................

PHX Based Clusters:
**Username:** PHX-POCxxx-User01 (up to PHX-POCxxx-User20), **Password:** *<Provided by Instructor>*

RTP Based Clusters:
**Username:** RTP-POCxxx-User01 (up to RTP-POCxxx-User20), **Password:** *<Provided by Instructor>*

Frame VDI
.........

Login to: https://frame.nutanix.com/x/labs

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** Credentials

Parallels VDI
.................

PHX Based Clusters Login to: https://xld-uswest1.nutanix.com

RTP Based Clusters Login to: https://xld-useast1.nutanix.com

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** Credentials

Employee Pulse Secure VPN
..........................

Download the client:

PHX Based Clusters Login to: https://xld-uswest1.nutanix.com

RTP Based Clusters Login to: https://xld-useast1.nutanix.com

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** Credentials

Install the client.

In Pulse Secure Client, **Add** a connection:

For PHX:

- **Type** - Policy Secure (UAC) or Connection Server
- **Name** - X-Labs - PHX
- **Server URL** - xlv-uswest1.nutanix.com

For RTP:

- **Type** - Policy Secure (UAC) or Connection Server
- **Name** - X-Labs - RTP
- **Server URL** - xlv-useast1.nutanix.com


Nutanix Version Info
++++++++++++++++++++

- **AHV Version** - AHV 20170830.337
- **AOS Version** - 5.11.2.3
- **PC Version** - 5.11.2.1
