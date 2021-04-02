.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_5:

---------------------------------------
Health Monitoring and Alerts
---------------------------------------

Creating a Performance Chart
+++++++++++++++++++++++++++++++++++++++++

In this exercise you will create a performance chart to monitor VM disk I/O.

#. If you are not logged into your Prism UI, log on now as the **admin** user.

#. From the **dashboard** drop down menu, click **Analysis**.

#. In the upper left of the UI, click **New** and then click **New Entity Chart**. An entity can be a host, a VM, a container and so on.

   .. figure:: images/1.png

#. Fill in the **New Entity Chart** fields as detailed below:

   * **Chart Title**: VM Disk Write I/O-<your initials>
   * **Entity Type**: Virtual Machine
   * **Entity**: CentOS
   * Metric: Storage Controller IOPS – Write

#. When you are done, the **New Entity Chart** should look similar to the screenshot below:

   .. figure:: images/2.png

#. Click **Save**.

#. Near the upper-right corner in the browser window, click the **Range** box and select **3 Hours**.

   .. figure:: images/3.png

Generating Write I/O
++++++++++++++++++++++++++

**Individual Exercise**

In this exercise you will configure a CentOS VM to write data to its local disk using the Linux command dd and monitor write IOPS on the performance chart you created in the previous exercise.

#. Go to the **VM** dashboard and select the **Table** tab.

#. Select the **CentOS-<your initials>** virtual machine. Power on the VM if necessary.

#. Click **Launch Console**.

#. Log on as the **root** user using the password **(See lab handout)**.

#. Generate I/O from the **CentOS-<your initals>** virtual machine by entering the following command (enter all of the following on a single line with no line breaks):

   .. code-block:: bash

     for ((i=1;i<=100;i++)); do dd if=/dev/zero of=/root/bigfile bs=64k count=500000 oflag=direct; done

   .. note::
     
    This command will write 500,000 64k blocks to the root directory repeating 100 times and takes from one to 10 hours to complete depending on the speed of the hardware you are using in the lab environment.

#. Go to the **Analysis** dashboard and view the **VM disk write I/O** graph. Refresh the URL to see the updated chart. You should see a green line to the far right sharply rise to denote the start of the dd operation. You can get a better view, shortening the time display, by going to the blue box at the top of the page and dragging the left side bar to the right to shorten the time sample.

   .. figure:: images/4.png

#. After observing for several minutes, press **<Ctrl-c>** to stop the writes. Close the console session.
