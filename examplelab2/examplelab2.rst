.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _example_lab_2:

---------------------------------------
Securing the Nutanix Cluster
---------------------------------------

Adding a User
++++++++++++++++

In this exercise you will work individually to add a local (i.e. non-domain) user account to your Nutanix cluster. This user will have permission to log on and perform cluster tasks based on the level of access granted to them.

#. Log on to your cluster’s Prism UI if needed.

#. Click the **gear** icon and scroll down the **Settings** column and select **Local User Management**.

#. In the **Local User Management window**, click **+ New User**.

   .. figure:: images/1.png

#. Use the data below to complete the fields in the **Create User** window:

   - Username: **Your user name**
   - First Name: **Your first name**
   - Last Name: **Your last name**
   - Email: **Your email address**
   - Password: **Use your full name with first letter capitalized and add /4u, eg:  Johnsmith/4u**
   - Language: **Your preferred language (e.g en-US)**
   - Roles: **Cluster Admin (You may need to scroll down)**

#. Click **Save**.

Verifying the New User Account
+++++++++++++++++++++++++++++++

#. Log out of the Prism interface by clicking the **Username** menu (next to the **gear** icon and is currently **admin**) and select **Sign Out**.

#. Log on to the Prism interface with the user account that you created in the previous exercise.

#. Observe your user account name (instead of admin) in the upper-right corner.

#. Click the **gear** icon, scroll down the **Settings** page and observe whether you can see and select **Local User Management**.

   Are you able to administer new user accounts?

   .. note::

    You should not be able to perform that action because the assigned Cluster Admin role does not have rights to administer user accounts.

#. Log out of Prism by clicking the Username menu and select Sign Out.
