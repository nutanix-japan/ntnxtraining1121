.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_12:

---------------------------------------
Monitoring a Nutanix Cluster
---------------------------------------

Using Nutanix Cluster Check (NCC) Health Checks
++++++++++++++++++++++++++++++++++++++++++++++++

In this exercise you will learn how to run NCC Health Checks in Prism Element UI. NCC Health Checks allows you to perform cluster health checks, collect cluster logs for Nutanix Support, as well as other useful functions.

#. Log into your Prism Element UI with the credentials provided in Cluster Configuration Guide.

#. Click on the main menu drop down and select HEALTH

   .. figure:: images/1.png

#. In the HEALTH page on the far right of the window, select Actions

   .. figure:: images/2.png

#. Select **Run NCC Checks**

#. In the menu review that the following parameters are as follows:

   Select checks you want to run:

   * All Checks (301): Ensure the radio button is **ON**
   * Only Failed and Warning Checks (1): **OFF**
   * Specific Checks: **OFF**
   * Send the cluster check report in the email: Uncheck Box

#. Click the **Run** to proceed with the NCC checks.

   .. note::
     As you are in a shared environment, a NCC health check might already been triggered and thus, you are prevented from running the task. You might need to wait for a couple of minutes before trying out again.

#. Once the check is run, proceed to the TASK menu and review the process. You should be done in under a couple of minutes.

   .. figure:: images/3.png

#. Click on the Succeeded highlighted link in the status to view the report and you should see the high level overview the report as shown below.

   .. figure:: images/4.png

#. Click on **Download Output** to view the health checks in detailed.

   .. figure:: images/5.png

#. Scroll through the text output to review the health checks.

Collecting Logs for Support
+++++++++++++++++++++++++++++++++

Nutanix Cluster Checks (NCC) includes the **Logbay** plug-in to collect the logs from Controller VM, host, masks the sensitive information like IP address, container names, etc. You can then upload these log bundles to an internal SFTP/FTP server to help Nutanix Support investigate any reported issues.

#. To view the various log collector options, enter the following command:

   .. code-block:: bash

    logbay collect --help

   .. figure:: images/6.png

#. As an example, to collect logs containing only cluster alerts, enter the following command:

   .. code-block:: bash

    logbay collect -t alerts

   .. figure:: images/7.png

   As you can see from the screenshot above, the output includes a line indicating the path to the tar file created that contains the alert logs from all the CVMs in the cluster.

#. As another example, to collect all logs for only the last day, enter the following command:

   .. code-block:: bash

    logbay_collect -t alerts --duration=24h0m0s

   .. figure:: images/8.png

#. The **Log Collector** option is also available through Prism.
#. From the **Health** dashboard, select **Actions** followed by **Log Collector**.

   .. figure:: images/9.png

#. Click **Run Now**.

#. While the health check tests are running, open the Prism **Tasks** dashboard to see the progress.

   .. figure:: images/10.png

Uploading Logs to Nutanix SFTP/FTP Server
++++++++++++++++++++++++++++++++++++++++++++++

.. note::
 The following section shows you how you can upload log files to Nutanix Support, you not not need to execute the commands display in this section

You can upload logs collected by logbay using internal SFTP or FTP server to help Nutanix Support to investigate the reported issues.

Nutanix recommends that you upload a file as a single zip or tgz (tarred and gzipped) file.

In the Controller VM, run one of the following command to upload log files to an internal SFTP or FTP server.

.. code-block:: bash

    nutanix@cvm$ logbay collect --dst=sftp://nutanix -c case_number
    nutanix@cvm$ logbay collect --dst=ftp://nutanix -c case_number

Replace case_number with the Nutanix support case number.

For example, the Controller VM SSH window displays results similar to the following.

.. code-block:: bash

    nutanix@cvm$ logbay collect --dst=sftp://nutanix -c 123456 -t stargate

    Time period of collection: Sun Dec 22 17:54:15 PST 2019 - Sun Dec 22 21:54:15 PST 2019
    Creating a task to collect logs...
    Logbay task created ID: x.x.x.x::4ba91e11-784c-4c8f-a37d-617d51ed2a45
    [====================================================================]
    x.x.x.x
    Archive Location: ftp.nutanix.com:123456/NTNX-Log-2019-12-22-1577080455-33287-PE-x.x.x.x-CW.zip
