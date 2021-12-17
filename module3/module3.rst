.. _m3:

------------------------------------
Centrify Privilege Elevation Service
------------------------------------

Privilege Elevation: Just Enough Privilege (Infrastructure Services)
********************************************************************
 
This exercise will walk you through Centrify Privilege Elevation Service. You will be able to grant just enough privilege for the users

#. Login as **afoster** in *Centrify* server 
#. Open **Access Manager** and naviagate to *Global Zone > Child Zone > Windows Zone > Computers > APPSERVER > Role Assignment*
#. Check that the **Role Assignment** is as below

   .. figure:: images/lab-002.png

#. If this is not the case, right-click on *Role Assigment* and select **Assign Role...**
#. Select the **Windows - Login Read Events** and select **OK**
#. Add the AD Group *OMICRON_GRP_Helpdesk* and click **OK** 
#. This will have added the group to the *Role Assignments*

#. Log in to the *AppServer* system as *JMiller*
#. When prompted for MFA, select *Security Question*. Answer: **Centrify**
#. Locate **Event Viewer** on the desktop and start it
#. Expand *Windows Logs* and click on **Security**
#. Note that Joe Miller is **unable** to see the Security logs from Event Viewer
#. *Right-click on Event Viewer* and select **Run with privilege**

   .. figure:: images/lab-001.png

#. Expand **Windows Logs** and click on **Security**
#. You will notice that the *Security* logs are now **visible** to you  
#. Without closing the current window, from the desktop, click on *Event Viewer* one more time *but do not run with privilege*. Simply double-click on it. Navigate to the *security* logs and notice that *you lost your privilege*. **The right to see the logs are only applicable when you run with privilege.**



Privilege Elevation: Just-In-Time Privilege (MFA Enabled)
*********************************************************
 
#. Log in to *Centrify* as Alex Foster (**afoster**)
#. Let's give the contractor Laura Bennet (*lbennet*) access to the *CloudVM* system. Open the *Admin Portal*
#. Login as **afoster** with the password *Centr1fy*
#. Navigate to *Resources > Systems*
#. Click the *CloudVM* system
#. Click **Permissions** and click **Add**
#. In the search bar type *Laura*, slect her account **LBennett@omicron..** and click **Add**

   .. figure:: images/lab-004.png

#. Click **Save**
#. Log out by clicking the name and select **Sign Out**

   .. figure:: images/lab-003.png

#. Login the portal as **lbennett** with the known password *Centr1fy*
#. Expand *Resources > Systems*
#. Locate *CloudVM*, right-click on it and select **Enter Account**
#. Login as **lbennett@omicron.lab** with *Cenr1fy* when prompted for User Name and Password
#. When prompted for MFA, select *Security Question*; Answer: **Centrify**
#. Once you are logged in, issue the command ``cat /etc/shadow``. Notice you do not have rights to see the content of the file.
#. Attempt utilizing the ``sudo cat /etc/shadow`` command and providing all requested follow up security questions, the system is telling that the user is not a part of the sudoers group and therefore, unable to run the command.

   .. figure:: images/lab-005.png

#. Open a Google Chrome *Incognito* screen
#. Open the Admin Portal by typing *centrifymember.omicron.lab* and login as **afoster**
#. Navigate *Settings > Resources > Global Workflow > Privilege Elevation Workflow*
#. Click **Add** and then set the first field *Approver Type* to **Requestor's Manager**
#. The second field *Action if user has no manager* to **Autmatically approve** (not the best idea, but this is for a lab.....)
#. Click **Add**

   .. figure:: images/lab-011.png

#. Click **Save**
#. Click on *CloudVM* and select *Workflow* and set *Privilege Elevation* to **Yes**
#. Once Privilege Elevation is set to yes, confirm **Requestor’s Manager** is one of the approvers for the request. Hit Save. Now, users that are not part of the sudoers group, will have the ability to request privilege as needed.
#. Return to the first Chrome Tab where lbennett is logged in.
#. Log in once again to the CloudVM
#. Issue ‘sudo cat /etc/shadow’
#. Now notice that Laura can elevate privilege based on a request
#. Follow the prompts on your screen and accept all defaults except the last step, Duration for request. Select number 3 [Temporary]. Since the request was automatically approved, user can now issue the command from step 16
#. Alternatively, we can provision the rights to this user permanently. Return to the tab where you logged in as Afoster. Expand Resources and click on Systems
#. Click on CloudVM and then Privilege Elevation. Locate the Add button and click on it
#. Type lbennett on the search bar. Select her account and click Add at the bottom
#. Repeat steps 14-16 and verify that user now has access to the /etc/shadow file


.. raw:: html

    <hr><CENTER>
    <H2 style="color:#80BB01">This concludes this lab</font>
    </CENTER>
