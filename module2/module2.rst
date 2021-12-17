.. _m2:

-------------------------------
Centrify Authentication Service
-------------------------------

Active Directory Bridging
*************************

Active Directory Bridging can be configured to permit Active Directory User Identities to log in to Linux/UNIX based systems without the need of local UNIX profiles.

| When a customer implements Centrify’s Active Directory components, they have a number of options available to them. These options provide the needed flexibility for an enterprise to move from local user accounts, with permissions managed via sudoer files, to a centralized administrative tool, such as Centrify Access Manager. Through Centrify Access Manager, administrators are able to select which users should have access to Linux/UNIX based systems within their network. The following steps will help familiarize you with this process and the many configuration options that are available.


#. Log into the Centrify Server as afoster
#. Open Active Directory Users and Computers, navigate beneath the omicron.lab domain to staff. Right-Click staff > New > User, and provide the following information:

   .. figure:: images/lab-001.png

   - First Name: Alex
   - Last Name: Bridge
   - User logon name: abridge@omicron.lab
   - Password: Centr1fy
   - Uncheck: User must change password at next logon
   - Check: Password never expires (we know… we know. It’s just for the lab)

#. Open the **Centrify Access Manager** shortcut on your desktop

   .. figure:: images/lab-002.png

#. Expand **Centrify Access Manager [DC.omicron.lab]**
#. Expand **Zones, Child Zones, Linux [Zone for Linux servers], Computers** 

   .. note::
       Within this child zone named Linux, you’ll see that we have one computer. This Centos8 system appears in this zone due to the successful install of a Centrify agent, which is providing the AD-Bridge function. Because it’s here, we can safely assume that a computer object has also been created within Active Directory, easily found within Active Directory Users and Computers. At this point, within Access Manager, Centrify administrators are able to create authentication and authorization rights for users so that they may interact with this system. In the following steps, we’ll begin to explore how this policy works.

#. Right-click **Centos8 > Show Effective User Rights**
#. Under the column *AD Name*, type in **Alex**

   .. note::
       You will notice that only one name appears (Alex Foster). You will see that Alex’s record shows a UID, Primary Group, GECOS, Home Directory, and more, including whether or not Alex requires MFA to login. The following steps will guide you through the provisioning of a UNIX profile for our new user, Alex Bridge, so that he too has system access.

#. Close out of the *Effective UNIX User Rights* window
#. Under *Child Zones > Linux > Unix*, right-click *Users*, and select **Add User**
#. Within the name field, type *Alex Bridge*
#. Select *Alex Bridge* from the results and then select **OK**

   .. note::
       We had previously mentioned that Centrify provides a number of configurable options for customers, allowing flexibility at time of original implementation and moving forward. These options here are often left default but can be modified to adapt these new capabilities into an environment where UID, Primary Group, etc, are of great importance and/or are critical for seamless integration with other systems. For now, we’ll keep the default

#. Select **OK**
#. Right-click **Centos8 > Show Effective User Rights**
#. Under the column *AD Name*, type in **Alex**

   .. figure:: images/lab-003.png

   .. note::
       You should still only see *Alex Foster* as the only Alex who has effective rights on this system. Let’s round out this exercise by granting login capabilities to Alex Bridge, later confirming that he has the ability to login.

#. Within the *Linux Child Zone*, expand **Authorization** (near the bottom)
#. Select **Role Assignment**

   .. note:: 
       Observe which Active Directory Security groups are assigned the *UNIX Login/Linux* role. You should see several, one of which is OMICRON_GRP_IT@omicron.lab. Instead of directly assigning Alex Bridge to the *UNIX Login/Linux* role, which results in more administrative overhead, we will now add Alex Bridge to the *OMICRON_GRP_IT* Active Directory Security Group, as that is his role in the organization.

       .. figure:: images/lab-004.png

#. Open **Active Directory Users and Computers**
#. Expand **omicron.lab > staff**
#. Right-click on *Alex Bridge* > **Properties > Member Of**
#. Add user to the group **OMICRON_GRP_IT**
#. Locate and start **PuTTY** from the Task Bar
#. When prompted, ready, select Ok for the next windows
#. Minimize **Active Directory Users and computers**, and return to **Access Manager**
#. Navigate back to *Child Zones > Linux*, and expand **Computers**
#. Right-click *Centos8* and select **Show Effective User Rights**

   .. figure:: images/lab-005.png

#. Open **PuTTY** and provide the host name **Centos8** 

   .. warning::
       DO NO USE THE SAVED SESSION AS THAT WILL USE AFOSTER AS THE USER.

       .. figure:: images/lab-007.png

#. CLick **Open**
#. Log in as *Alex Bridge (abridge)*
#. You will be prompted for your **Active Directory Password**. Input the right password (*Centr1fy*) and you will successfully log in to the Linux environment with an Active Directory account

   .. figure:: images/lab-008.png

#. Search for the root account in the /etc/passwd file; ``grep root /etc/passwd``
#. Look for **abridge** in the same file; ``grep abridge /etc/passwd``
#. Nothing should return for *abridge* since it is **not a local account**
#. Repeat the exercise but this time log in as **Laura Bennett (lbennett)**
#. Centrify supports Kerberos authentication. Locate and start PuTTY from the Task Bar and select **CentOS 8** by double clicking it
 
   .. note::
       Optional: Run the id command to verify UID and GID for the user.
       
       | Optional: To verify the roles users have been granted through Centrify, run the Centrify command ``dzinfo``

 


Centrify Brokered Authentication Service
****************************************
 
Centrify allows you to authenticate with cloud/dmz instances by leveraging Active Directory users. MFA can also be implemented, as well as session monitoring and recording. (Talk about how it works)

#. Log in to the **Centrify** server as **afoster**, start PuTTY, and Log in to *CloudVM* as **root**
#. Issue ``ifconfig ens34`` and note the network information
#. This system is not joined to omicron.lab and it is in a different network *192.168.0.100/24* (simulating cloud instances)
#. Exit the session as root and *start* a new session. Log in as **afoster**

   .. figure:: images/lab-009.png

#. You will notice that you were *prompted for MFA* and that you were able to login with an **Active Directory User afoster**
#. **Close** the session by closing the *PuTTY* window
#. Log in to the *Centrify* server as **afoster** and open the **Admin Portal**
#. Expand *Resources*, click on *Systems*, and click on **Cloud VM**
#. Right-click on **ec2user** and select **Login**. A session will start without the need for further authentication. You are now logged in as the local ec2user

   .. figure:: images/lab-010.png

 


Managing Users Through AD
*************************

This lab will demonstrate how to manage users through Active Directory.

#. Log in to *Centrify* as **afoster**
#. Locate **Access Manager** on your desktop and start it
#. Expand the *Global Zone, Child Zones, Linux Zone, and Authorization*
#. Click on **Role Assignments**
#. Under the **Assignee** column, note that roles are associated with AD users and AD groups
#. Right-click *OMICRON_GRP_IT@omicron.lab* and select **AD Properties**

   .. figure:: images/lab-011.png

#. Click on the **members** tab to see what users belong to this Active Directory Group. All these users have Login rights over the systems in this Centrify Zone (in this case, only one system)
#. We are going to *add* a user to *OMICRON_GRP_IT* in Active Directory. Open *Active Directory Users and Computers*, right-click on *omicron.lab*, and select **Find**
#. Type **Li Wang** and click **Find Now**
#. Once user is located, *right-click on the user* and select **Add to a group**

   .. figure:: images/lab-012.png

#. Select the *OMICRON_GRP_IT* and click **OK**

   .. figure:: images/lab-013.png

#. Return to *Access Manager*, expand *Linux Zone, Computers*, *right-click CentoOS 8*, and select **Show Effective User Rights**
#. Li Wang should now have log in rights for CentOS 8
#. Locate and *start PuTTY* from the Windows Task Bar, provide **CentOS 8** as the host and open the connection
#. Log in as **root**
#. Flush the cache by issuing ``adflush``. The caching time is customizable. *Exit the session*
#. Once again, *start PuTTY*, provide **CentOS 8** as the host and open the connection 
#. Log in as Li Wang (**lwang**). Use the default password *Centr1fy*
#. Type ``dzinfo`` to obtain more information about the user roles managed by Centrify Access Manager
#. Now, exit the session with Li Wang
#. Return to *Active Directory Users and Computers*, right-click the domain *omicron.lab*, and select **Find**
#. Type *Li Wang* and click **Find Now**
#. Once the user is located, *right-click user* and select **Disable Account**
#. *Open PuTTY*, provide **CentOS 8** as the host and open the connection
#. Attempt to log in as **lwang**. Use the default password *Centr1fy*

   .. figure:: images/lab-014.png

   .. Note::
       Note that the user is unable to log in. Re-enable the account in Active Directory.


       
MFA at Login (\*NIX)
********************

In this exercise, you can enforce MFA at the login screen on a Linux/UNIX system, using security questions. Additional MFA options are available and can be enforced. Speak with your Centrify Systems Engineer regarding these additional MFA options that may be implemented.
 

#. Log in to the *Centrify* server as **afoster**
#. Locate **Access Manager** on your desktop and start it
#. Expand *Global Zone, Child Zones, Linux Zone, and Computers*
#. Right-click *CentOS 8* and select **Show Effective User Rights**. There will be a list of users that have privileges to access this system
#. Look for **lbennett**. Note that it says **True** under the *Require MFA* column

   .. figure:: images/lab-015.png

#. Open PuTTY, provide **CentOS 8** as the host and open the connection
#. At the login prompt, type **lbennett**
#. Provide the Active Directory Password when prompted (*Centr1fy*)
#. Note the MFA prompt
#. Select the *Security Question* option (number 2), and answer: **Centrify**

   .. figure:: images/lab-016.png

MFA at Login (Windows)
**********************

In this exercise, you can enforce MFA at the login screen on a Windows system using security questions. Additional MFA options are available and can be enforced. Speak with your Centrify Systems Engineer regarding these additional MFA options that may be implemented.
 

#. Log in to *Centrify* as **afoster**
#. Locate **Access Manager** on your desktop and start it
#. Expand the *Global Zone, Child Zones, Windows Zone, and Computers*
#. *Right-click on the Appserver* system and select **Show Effective User Rights**
#. There will be a list of users that have privileges to access this system. Look for *JMiller*. Note that it says True under the Require MFA column

   .. figure:: images/lab-017.png

#. Log in to the *AppServer* system as **JMIller**. Use the default password *Centr1fy*
#. On the MFA prompt, select Security Question. Answer: **Centrify**

   .. figure:: images/lab-018.png

#. Once logged in, go to *Google Chrome* and access **Centrify.com**
#. Leave this section open and proceed to the next exercise
 

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#80BB01">This concludes this lab</font>
    </CENTER>
