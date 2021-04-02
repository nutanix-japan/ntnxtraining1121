.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_11:

-------------
Prism Central
-------------

Working with Prism Central
++++++++++++++++++++++++++

You will work through the lab using Prism Central interface. Your cluster can only be registered to one Prism Central Server at a time.

#. In Prism Element UI, ensure that you see the screenshot that displays Prism Central status as **OK**.

   .. figure:: images/1.png

#. In the **Prism Central** widget, click **Launch**.

#. A new browser tab should open. Log on to Prism Central with the **admin** user. Prism Central displays the **Main** dashboard.

   .. figure:: images/2.png

Using Prism Central's Basic Features
+++++++++++++++++++++++++++++

In this exercise you will explore some of basic features of Prism Central.

#. If needed, log on to Prism Central and access the **Main** dashboard.

   How many clusters are registered with this Prism Central instance?

#. Click on your cluster name from any widget where it is listed (you may need to refresh your browser). This will take you to the **Clusters Summary** page.

   .. figure:: images/3.png

#. Explore the links down the left side of the browser window to see what information has been imported to the Prism Central database. When finished, click the Nutanix **X** in the upper middle of the UI to return to the **Main** dashboard.

Creating a Custom Dashboard
+++++++++++++++++++++++

In this exercise you will create a custom dashboard.

#. If necessary, log on to Prism Central.

#. At the upper left, click **Manage Dashboards**.

#. In the pop-up, click **+New Dashboard**.

#. Type a name for the dashboard (i.e. HPE-<your initials>), then click **Save**.

   .. figure:: images/4.png

#. When you click on the new dashboard name, you should see a blank page and the option to **Add Widgets**.

   .. figure:: images/5.png

#. Click on the **Add Widgets** link in the middle panel or on the add widgets icon at the upper right.

#. In the left panel, select the **Cluster Quick Access** widget from the list of predefined widgets.

   At the lower right, click **Add to Dashboard**.

   .. figure:: images/6.png

#. From the left panel, select the **Custom Chart Widget** and create a custom widget. In the right panel, experiment with the configuration options to define a widget to your needs.

   .. Note::
    When you click in the Entity Search field the options available for selection are based on the Entity Type setting.

   .. figure:: images/7.png

#. When completed, click **Add & Return to Dashboard** at the lower right to display your finished dashboard.

   .. figure:: images/8.png

Creating a Custom Report
++++++++++++++++++++++++++

**Group Exercise**

In this exercise you will create a custom report using Prism Central.

#. From the **Main** dashboard, click the hamburger menu (the three-lined icon) in the upperleft corner of the browser window. This will display dashboard options on the left side of the browser.

   .. figure:: images/9.png

#. In the **dashboard** menu, hover over **Operations** and then click **Reports**.

   .. figure:: images/10.png

#. Click the **Cluster Efficiency Summary** check box and click the **Actions** menu above.

#. Select **Run** from the menu to display the **Run Report** window. Populate the empty fields as follows:

   * Report Instance Name: **<your initials>-PC-Report**
   * Description: Enter any text you would like
   * Time Period For Report: **Last 24 hours**
   * Report Format: **PDF**
   * Additional Recipients: Leave this field blank

#. Click **Run**.

#. Click the **Cluster Efficiency Summary** report name (click the text on the report name not the check box). You should see the PDF instance of the report you have just run.

   .. figure:: images/11.png

#. Click the **PDF** link to download the PDF report. This will be saved to the downloads folder on your VDI desktop.

#. Open the downloaded PDF to view the report.

#. Scroll through the report to see what information it contains.

   .. Note::
    Your Prism Central instance has only been running a short time and may not show any data in the report’s graphs and other widgets. Typically,

   You would run reports after Prism Central has been running for several days or weeks.

#. Close the **Cluster Efficiency Summary** page and click the X on the top bar to return to the **Main** dashboard.

Creating a "What-If" Scenario
+++++++++++++++++++++++++++++

In this exercise you will explore how to create a planning session to forecast future needs based on current growth.

#. From the **Prism Central Main** dashboard, click the hamburger menu at the upper left and select **Operations -> Planning**.

   .. figure:: images/12.png

#. At the upper right, click **New Scenario** to open the **Scenario Definition** tab.

   .. figure:: images/13.png

#. In the left panel, select your cluster from the **Cluster** drop down menu.

#. In the **Target** box, select **12 months**.

#. In the right panel area, under **Resources**, you can choose **Add/Adjust** to define your nodes and node configurations. Review the options and keep the existing hardware setting.

#. In the left panel, check the **Capacity Configuration** box to modify or add reservation on cluster capacity.

   .. figure:: images/14.png

#. In the left panel next to **Workload**, click **Add/Adjust** to add or adjust the workload that will be placed on the cluster with the following values:

   .. figure:: images/15.png

   Scroll down and enter **500** into the **Number of Users** text box.

#. Click **Save**. The saved VDI configuration is shown in the left panel and the check box to **display the scenario** will already be selected. Click **Recommend** to review the recommendations (if any).

   .. figure:: images/16.png

#. Click the **Save Scenario** button to save the scenario.

   .. figure:: images/17.png
