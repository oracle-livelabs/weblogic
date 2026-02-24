# Create Security Groups, Roles, Aliases and Accounts

## Introduction

This lab will show you how to install Oracle WebCenter Content Administration Desktop Client and create Security Groups, Roles, Aliases and Accounts in WCC

**Estimated Lab Time**: *45 minutes*

### Objectives

- Download and install Oracle WebCenter Content Administration Desktop Client
- Create Security Group
- Create Role
- Map Roles to Security Group
- Create Alias
- Create Account

### Prerequisites

This lab assumes you have:

- Access to WCC Marketplace Environment

This lab assumes you have completed:

- Lab: Initialize WCC Environment
- Lab: Create Users and Groups

## Task 1: Download and install Oracle WebCenter Content Administration Desktop Client

 To Install WebCenter Content Administration Desktop Client, follow the below steps;

1. Login to WebCenter Content server as user with Administrator Privilege, Under **Administration** tab, navigate to **Admin Applets**. Click on **Download Client** button. This downloads wccadmin-installer.msi file on windows and wccadmin-installer.dmg file on mac
![This image shows the WCC Administration Applets Page](./images/task1-webcenter-admin-applet.png "WCC Administration Applets Page")

2. Install the wcc admin client:

<if type="MAC">

- Double click on downloaded wccadmin-installer.dmg
- Move the **Oracle WebCenter Content Administration** to **Applications**
 ![This image shows the WCC Administration Application](./images/webcenter-admin-application.png "WCC Administration Application")

</if>

<if type="Windows">

- Double click on downloaded wccadmin-installer.msi
 ![This image shows the WCC Administration Client Installer](./images/wcc-install-progress.png "WCC Administration Client Installer")

 > Wait for the installation to complete
</if>

## Task 2: Configure Oracle WebCenter Content Administration Desktop Client

To Configure WebCenter Content Administration Desktop Client, follow the below steps;

1. Launch WebCenter Content Administration Desktop Client.

<if type="Windows">

- In Windows Start menu search **Oracle WebCenter Content Administration**
- Click on **Oracle WebCenter Content Administration** app
 ![This image shows the WCC Administration Desktop Client](./images/wcc-admin-installed.png "WCC Administration Desktop Client")
</if>

<if type="MAC">

- In Mac **Spotlight search** search **Oracle WebCenter Content Administration**
- Click on **Oracle WebCenter Content Administration** app
 ![This image shows the WCC Administration Desktop Client](./images/webcenter-admin-launch-mac.png "WCC Administration Desktop Client")
</if>

2. Enter the **User Name, Password, Server**. Click **OK**.
   - **User Name**: Enter
         ```
         <copy>weblogic</copy>
         ```
   - **Password**: Enter
         ```
        <copy>Welcome1</copy>
         ```
   - **Server**: Enter
         ```
         <copy>https://localhost:16200/cs/</copy>
         ```
    > Note : Replace `"https://localhost"` with your **hosturl** ( eg: `"http://wcc-document-livelab.livelabs.oraclevcn.com"` or `"https://192.0.0.0"`)

![This image shows the WCC Administration Desktop Client Login Screen](./images/webcenter-admin-login.png "WCC Administration Desktop Client Login")
3. If **Warning** dialog is opened due to insecure certificate, press **Yes** to continue.
![This image shows the WCC Administration Desktop Client Warning](./images/webcenter-admin-warning.png "WCC Administration Desktop Client Warning")
4. Wait for WebCenter Content Administration Dialog to open
![This image shows the WCC Administration Applets](./images/webcenter-admin-applet.png "WCC Administration Applets")

## Task 3: Create Security Group

To create Security Groups (HRAdministrator\_SG, HRRepresentatives\_SG) in WCC follow these steps:

1. Login to WebCenter Content Administration Desktop Client as user with Administrator Privilege.
2. Click on **User Admin** Link
![This image shows the WCC Administration Applets](./images/webcenter-admin-applet.png "WCC Administration Applets")
3. Select **Security** > **Permissions by Group...** menu
![This image shows the WCC Administration User Admin](./images/webcenter-admin-user-admin-group.png "WCC Administration User Admin")
4. Click on **Add Group...** button
![This image shows the WCC Administration Permissions By Group](./images/webcenter-admin-permissions-by-group.png "WCC Administration Permissions By Group")
5. Enter the **Group Name** and **Description**. Click **OK**.
   - **Group Name**: Enter
         ```
        <copy>HRAdministrator_SG</copy>
         ```
   - **Description**: Enter
         ```
        <copy>HRAdministrator_SG</copy>
         ```
![This image shows the WCC Administration Add Group](./images/webcenter-admin-add-group.png "WCC Administration Add Group")
6. Similarly create Security Group HRRepresentatives\_SG.

## Task 4: Create Role

To create Roles (HRAdministrator and HRRepresentatives - These role names are same as groups in IDCS/Weblogic realm) in WCC follow these steps:

1. Login to WebCenter Content Administration Desktop Client as user with Administrator Privilege.
2. Click on **User Admin** Link
![This image shows the WCC Administration Applets](./images/webcenter-admin-applet.png "WCC Administration Applets")
3. Select **Security** > **Permissions by Role...** menu
![This image shows the WCC Administration User Admin](./images/webcenter-admin-user-admin-role.png "WCC Administration User Admin")
4. Click on **Add New Role...** button
![This image shows the WCC Administration Permission By Role](./images/webcenter-admin-permissions-by-role.png "WCC Administration Permission By Role")
5. Enter the **Role Name** and **Role Display Name**. Click **OK**.
    - **Role Name**: Enter
          ```
          <copy>HRAdministrator</copy>
          ```
    - **Role Display Name**: Enter
          ```
          <copy>HRAdministrator</copy>
          ```
![This image shows the WCC Administration Add Role](./images/webcenter-admin-add-new-role.png "WCC Administration Add Role")
6. Similarly create Role HRRepresentatives.

## Task 5: Map Roles to Security Group

To Map Roles to Security Groups in WCC follow these steps:

1. Login to WebCenter Content Administration Desktop Client as user with Administrator Privilege.
2. Click on **User Admin** Link
![This image shows the WCC Administration Applets](./images/webcenter-admin-applet.png "WCC Administration Applets")
3. Select **Security** > **Permissions by Group...** menu
![This image shows the WCC Administration User Admin](./images/webcenter-admin-user-admin-group.png "WCC Administration User Admin")
4. Select on **HRAdministrator_SG** group from "Groups" List. Select **HRAdministrator** Role from "Roles" List and click **Edit Permissions...** button
![This image shows the WCC Administration Permission by Group](./images/group-role-mapping.png "WCC Administration Permission by Group")
5. Click on **Admin** in **Edit Permission** Screen and click **OK**
![This image shows the WCC Administration Edit Permission](./images/edit-permission.png "WCC Administration Edit Permission")
6. Similarly assign Permissions to other Security Group and Role Combination

| Security Group | Role | Maximum Permission |
| ----------- | ----------- |
| HRAdministrator\_SG | HRRepresentatives | Read |
| HRRepresentatives\_SG | HRAdministrator | Admin |
| HRRepresentatives\_SG | HRRepresentatives | Delete |
{: title="Security Group-Role mapping"}

## Task 6: Create Alias

To create Alias in WCC follow these steps:

1. Login to WebCenter Content Administration Desktop Client as user with Administrator Privilege.
2. Click on **User Admin** Link
![This image shows the WCC Administration Applets](./images/webcenter-admin-applet.png "WCC Administration Applets")
3. Select **Aliases** tab and click **Add**
![This image shows the WCC Administration Alias](./images/webcenter-admin-aliases.png "WCC Administration Alias")
4. Enter the **Alias Name, Alias Display Name and Description**. Click **Add..**
    - **Alias Name**: Enter
           ```
          <copy>TrainingReps</copy>
           ```
    - **Alias Display Name**: Enter
           ```
          <copy>TrainingReps</copy>
           ```
    - **Description**: Enter
           ```
           <copy>Training Representatives</copy>
           ```
![This image shows the WCC Administration Add New Alias](./images/webcenter-admin-add-new-alias.png "WCC Administration Add New Alias")
5. In **Select Users** dialog, click **Define Filter...**
![This image shows the WCC Administration Select Users](./images/webcenter-admin-select-user.png "WCC Administration Select Users")
6. In **Define Filter** dialog select Only **User Name** field and Enter **Training%** in User Name Field. Click **OK**
![This image shows the WCC Administration Define Filter](./images/webcenter-admin-define-filter.png "WCC Administration  Define Filter")
7. Select TrainingRep1 to TrainingRep4 and Click **OK**
![This image shows the WCC Administration Select User](./images/webcenter-admin-alias-add-users.png "WCC Administration Select User")
8. Click **OK** in **Add New Alias** dialog.

## Task 7: Create Account

To create Account in WCC follow these steps:

1. Login to WebCenter Content Administration Desktop Client as user with Administrator Privilege.
2. Click on **User Admin** Link
![This image shows the WCC Administration Applets](./images/webcenter-admin-applet.png "WCC Administration Applets")
3. Select **Security** > **Predefined Accounts...** menu
![This image shows the WCC Administration User Admin](./images/webcenter-admin-user-admin-account.png "WCC Administration User Admin")
4. Click on **Add...** button
![This image shows the WCC Predefined Accounts](./images/predefined-accounts.png "WCC Administration Predefined Accounts")
5. Enter the **Predefined Account**. Click **OK**.
     - **Predefined Account**: Enter
           ```
           <copy>Training</copy>
           ```
![This image shows the WCC Add Accounts](./images/add-new-account.png "WCC Administration Add Accounts")

You may now **proceed to the next lab**.

## Acknowledgements

- **Authors-** Sujata Nayak, Consulting Member Technical Staff, Oracle WebCenter Content
- **Contributors-** Sujata Nayak, Senthilkumar Chinnappa, Mandar Tengse , Parikshit Khisty
- **Last Updated By/Date-** Sujata Nayak, December 2024
