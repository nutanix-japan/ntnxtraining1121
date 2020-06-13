.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_6:

-------------
Distributed Storage Fabric
-------------

Creating a Performance Chart
+++++++++++++++++++++++++++++++++++++++++
In this exercise you will create a performance chart to monitor VM disk I/O.

1.  If you are not logged into your Prism UI, log on now as the **admin** user.

2.  From the **dashboard** drop down menu, click **Analysis**.

3.  In the upper left of the UI, click **New** and then click **New Entity Chart**. An entity can be a host, a VM, a container and so on.

   .. figure:: images/1.png
 
4.  Fill in the **New Entity Chart** fields as detailed below:

 * **Chart Title**: VM Disk Write I/O-<your initials>
 * **Entity Type**: Virtual Machine
 * **Entity**: CentOS
 * Metric: Storage Controller IOPS – Write

5.  When you are done, the **New Entity Chart** should look similar to the screenshot below:
 
   .. figure:: images/2.png

6.  Click **Save**.
7.  Near the upper-right corner in the browser window, click the **Range** box and select **3 Hours**.

   .. figure:: images/3.png
 
Generating Write I/O
++++++++++++++++++++++++++

**Individual Exercise**

In this exercise you will configure a CentOS VM to write data to its local disk using the Linux command dd and monitor write IOPS on the performance chart you created in the previous exercise. 

1.  Go to the **VM** dashboard and select the **Table** tab.

2.  Select the **CentOS-<your initials>** virtual machine. Power on the VM if necessary.

3.  Click **Launch Console**.

4.  Log on as the **root** user using the password **(See lab handout)**.

5.  Generate I/O from the **CentOS-<your initals>** virtual machine by entering the following command (enter all of the following on a single line with no line breaks):

  .. code-block:: bash

     for ((i=1;i<=100;i++)); do dd if=/dev/zero of=/root/bigfile bs=64k count=500000 oflag=direct; done
  
  .. Note::
   This command will write 500,000 64k blocks to the root directory repeating 100 times and takes from one to 10 hours to complete depending on the speed of the hardware you are using in the lab environment.

6.  Go to the **Analysis** dashboard and view the **VM disk write I/O** graph. Refresh the URL to see the updated chart. You should see a green line to the far right sharply rise to denote the start of the dd operation. You can get a better view, shortening the time display, by going to the blue box at the top of the page and dragging the left side bar to the right to shorten the time sample.

   .. figure:: images/4.png
 
7.  After observing for several minutes, press **<Ctrl-c>** to stop the writes. Close the console session.
