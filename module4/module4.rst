.. _m4:

-------------------------------------
Centrify Audit and Monitoring Service
-------------------------------------

In this exercise, you will watch audited sessions recorded using the Centrify Audit and Monitoring Service. You will be shown how to create queries to find specific items and create reports  for  a  transparent  understanding  of  what  users  have  done  in  the environment.

Session Recording and Auditing
******************************
 
Some of the sessions you went through today were recorded. You will be able to locate these sessions and watch them

#. Log in to the *Centrify* server as **afoster**
#. Open the *Centrify Portal* by clicking on the *Admin Portal* shortcut on the desktop and login as **afoster**
#. Expand *Systems > Resources*
#. Click on **CentOS 8**
#. Right-click on the local account **centrify** and select **Login**
#. Issue a few commands (top, vmstat, ps aux). Exit the session using **CTRL+d** and **Close**

   .. figure:: images/lab-001.png

#. Minimize the Portal
#. Locate *Audit Analyzer* on your desktop and start it. 

   .. figure:: images/lab-002.png

#. Click **Yes** when prompted from the UAC
#. Under *Audit Sessions*, look for **Today**, and click on it. You should see the sessions you worked on today as you progressed through the labs

   .. figure:: images/lab-003.png

#. Watch the session from *Alex Foster* when he logged in as the **local user centrify** on the *CentOS 8* server **(10.160.0.148)**. Double-click to watch

   .. figure:: images/lab-004.png

   .. Note::
        The logs on the left pane as you watch the recorded sessions. You should see the commands you issued earlier. You will have the ability to click on them and jump to specific point in time.
        
        | This session was recorded from the Centrify Portal and this feature is called Gateway Session Recording. Now, exit the Centrify Audit and Monitoring Service window.
       
        .. figure:: images/lab-005.png

#. Close the *Centrify DirectWatch* session

Host-Based Session Auditing and Video Capture
*********************************************
 
Let’s now watch a Windows session. This next session was recorded when the user connected directly to the server, circumventing the Centrify Portal (vault).

#. Select any session from Joe Miller on the AppServer system

   .. figure:: images/lab-006.png

#. Double-click on the session and watch your activities. Notice the left pane and all the events from your session
#. Close the *Centrify DirectWatch* session

Session Auditing
****************
 
#. Right-click *Audit Session* and select **New Quick Query**.

   .. figure:: images/lab-007.png

#. For the query criteria, type *dzinfo*, and click **Find**
#. Under *Audit Session*, you will notice a new item called **Quick Queries**. Click on it to see the sessions that match the specified criteria (*dzdo*)

   .. figure:: images/lab-008.png

   .. note::
       More robust queries can be created. Consult a Centrify Systems Engineer and ask about Private Queries
 
Reports
*******
 
#. In *Audit Analyzer*, expand **Reports**
#. Right-click on *User Activity Report* and select **Create New Report**

   .. figure:: images/lab-009.png

#. Leave the *Query criteria* as default. Click on **Show Report**
#. A report containing user activity is now available to you
#. You can save the report in many formats (HTML, PDF, CSV, XML) or email it as desired

   .. figure:: images/lab-010.png

#. Close **Audit Analyzer**

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#80BB01">This concludes this lab</font>
    </CENTER>
