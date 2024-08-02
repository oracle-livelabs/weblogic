# Setup RFP Management APEX Application


## Introduction

In this lab, you learn to install and run Oracle APEX Application for RFP Management System. 

This lab also covers updating the APEX Rest Datasource urls & credentials for connecting to WebCenter Content Instance

Estimated Time: 20 minutes

### Objectives
In this lab, you will:
- Navigate through Oracle APEX
- Create New Workspace
- Login to Workspace and Install Packaged Application.
- Update Rest Datasources URL and credentials

## Task 1: Create New APEX Workspace for RFP Management Application

To create new APEX workspace, you need log in to Oracle APEX's default **INTERNAL** Workspaces as **ADMIN** User (or) the user with Administrator Privilege on the APEX Instance

1. On the new *web browser* window , Login to the APEX/ORDS URL as **ADMIN** User of System's **INTERNAL** Workspace. Details are provided below

    - URL

    ```
    <copy>http://localhost:16200/ords/</copy>
    ```

- Workspace Name

    ```
    <copy>INTERNAL</copy>
    ```

    - Username

    ```
    <copy>ADMIN</copy>
    ```

    - Password

    ```
    <copy>WelCwcm123##</copy>
    ```

    > **For ATP DB** *, ADMIN password is same as the ADMIN DB schema user password*

    > _If any issues with ADMIN credentials, Refer to **Appendix 3: Reset ADMIN password for APEX/ORDS** of the previous lab **Initialize WCC Environment** to reset ADMIN Password_

    ![This image shows the APEX/ORDS Login Page](./images/apex_login_internal.png "APEX/ORDS Login Page")


2. In the *Administration Services* Landing page , Click on **Create Workspace** button on the top right corner

    ![This image shows the APEX/ORDS Landing Page](./images/apex_create_workspace_homepage.png "APEX/ORDS Landing Page")

3. Provide the value for **Workspace Name**  and click **Next** Button

    ```
    <copy>WCCRFPMGMT</copy>
    ```

 ![This image shows the APEX/ORDS Create Workspace Page](./images/apex_create_workspace_step1.png "APEX/ORDS Create Workspace Page")

4. Provide the values for DB Schema details as mentioned below and click **Next** Button

    * **Re-use existing schema?**: Select **No**

    * **Schema Name**: Enter
    ```
    <copy>WCCRFPMGMT_SCHEMA</copy>
    ```
    * **Schema Password**: Enter
    ```
    <copy>WelCwcm123##</copy>
    ```
    * **Space Quota (MB)**: Select **500**

 ![This image shows the APEX/ORDS Create Workspace Page 2 - DB Schema Details](./images/apex_create_workspace_step2.png "APEX/ORDS Create Workspace Page 2 - DB Schema Details")

5. Provide the values for Workspace **ADMIN** User details as mentioned below and click **Next** Button

    * **Administrator Username**: Enter
    ```
    <copy>ADMIN</copy>
    ```
    * **Administrator Password**: Enter
    ```
    <copy>Welcome1</copy>
    ```
    * **First Name**: Enter
    ```
    <copy>Admin</copy>
    ```
    * **Last Name**: Enter
    ```
    <copy>User</copy>
    ```
    * **Email**: Enter your email id
    ```
    <copy>admin_user@email.com</copy>
    ```
 ![This image shows the APEX/ORDS Create Workspace Page 2 - Admin User Details](./images/apex_create_workspace_step3.png "APEX/ORDS Create Workspace Page 2 - ADMIN User Details")

6. Review the details and click **Create Workspace** Button

 ![This image shows the APEX/ORDS Create Workspace Page](./images/apex_create_workspace_step4.png "APEX/ORDS Create Workspace Page")

7. After the workspace is successfully created, it will display  workspace details.  click **Done** Button

 ![This image shows the APEX/ORDS Workspace Created Page](./images/apex_create_workspace_step5.png "APEX/ORDS Workspace Created Page")


## Task 2: Login to Newly Created APEX Workspace


To log in to Oracle APEX, you need a Workspace Name, username, and the password created for that Workspace. In this hands-on lab, you log in to your Oracle APEX Workspace.

1. To login to your Oracle APEX Workspace, perform the following steps:
    -	Open your browser and enter the **URL** to sign in to the APEX development environment.

    - The login page appears. Enter the **Workspace Name, Username, and Password**. Click **Sign In**.  

    * **Workspace Name**: Enter
    ```
    <copy>WCCRFPMGMT</copy>
    ```
    * **Username**: Enter
    ```
    <copy>ADMIN</copy>
    ```
    * **Password**: Enter
    ```
    <copy>Welcome1</copy>
    ```
  ![Workspace Login](images/apex_login_workspace_step1.png "Login to APEX Workspace")


2. If its first time Login, Change password for the ADMIN user. You can provide the same Password value and click on **Change Password**.
    > Skip this step if it does not prompt for Change Password

    * **New Password**: Enter
    ```
    <copy>Welcome1</copy>
    ```
    * **Confirm Password**: Enter
    ```
    <copy>Welcome1</copy>
    ```

  ![Reset Password on First Login Page](images/apex_login_workspace_step2.png "Reset Password on First Login")

3. The Workspace home page appears.

  ![Workspace Home Page](images/apex_login_workspace_step3.png "Workspace Home Page")


## Task 3: Install RFP Management Application

This task covers installing and running a WCC RFP Management System APEX application.

1. Edit the downloaded APEX Application sql file **wcc-rfp-mgmt-system-apex-app.sql** in a text editor (eg: Notepad) , replace **localhost** with the hostname of the wcc instance () eg: **wccrfpmgmtdemo.oraclevcn.com** ) and save the file as file **wcc-rfp-mgmt-system-apex-app_<your_wcc_hostname>.sql** ( eg: *wcc-rfp-mgmt-system-apex-app_**wccrfpmgmtdemo**.sql* )

![Edit in Notepad](images/apex_task3_step0_1.png "replace localhost with <your_wcc_hostname> ")

![Save File As ](images/apex_task3_step0_2.png "Save File ")

2. After Login to the WORKSPACE **WCCRFPMGMT** as ADMIN user, in the Home Page, Under  **Apex Builder** , click on **Import**

  ![App Builder](images/apex_task3_step1.png "App Builder > Import ")


3. Select the updated file **wcc-rfp-mgmt-system-apex-app_<your_wcc_hostname>.sql** ( eg: *wcc-rfp-mgmt-system-apex-app_wccrfpmgmtdemo.sql* ) , ensure that the **File Type** is selected as **Application, Page or Component** and click **Next** Button

  ![Application sql file import](images/apex_task3_step2.png "WCC RFP Management APEX Application Import Page")

4. In the **Install Application** Page, Verify the below values and click **Install Application** Button

  * *Current Workspace* : **WCCRFPMGMT**
  * *Parsing Schema* : **WCCRFPMGMT_SCHEMA**
  * *Build Status* : **Run and Build Application**
  * *Install as Application* : **Auto Assign New Application ID**

  ![Install Application Page](images/apex_task3_step3.png "WCC RFP Management APEX  - Install Application Page")

5. In the **Install Application** - **Credentials** Page, for **Credentials for WCC RFP Mgmt**, Update the values for the below and click **Next** Button

    * **Client ID or Username** : Enter
    ```
    <copy>weblogic</copy>
    ```
    * **Client Secret or Password** : Enter
    ```
    <copy>Welcome1</copy>
    ```
    * **Verify Client Secret / Password** : Enter
    ```
    <copy>Welcome1</copy>
    ```

  ![Install Application - Credentials Page](images/apex_task3_step4.png "WCC RFP Management APEX  - Install Application - Credentials Page")

6. After the Credentials is updated, in the **Application Installed** Page, click on **Install Supporting Objects** button

  ![Application Installed - Install Supporting Objects](images/apex_task3_step5.png "WCC RFP Management APEX  - Application Installed - Install Supporting Objects")

7. After the Supporting Objects installed, click on **Install Summary** button , to view the status of the Supporting objects installation

  ![Supporting Objects Installed](images/apex_task3_step6.png "WCC RFP Management APEX Application - Supporting Objects Installed")




## Task 4: Import REST DataSource Catalog

This task covers importing and configuring Rest Datasource Catalog.


1. Edit the downloaded APEX Application sql file **WCC_RFP_Rest_Catalog.sql** in a text editor (eg: Notepad) , replace **localhost** with the hostname of the wcc instance () eg: **wccrfpmgmtdemo.oraclevcn.com** ) and save the file as  **WCC_RFP_Rest_Catalog_<your_wcc_hostname>.sql** ( eg: *WCC_RFP_Rest_Catalog_**wccrfpmgmtdemo**.sql* )

![Edit in Notepad](images/apex_task4_step0_1.png "replace localhost with <your_wcc_hostname> ")

![Save File As ](images/apex_task4_step0_2.png "Save File ")

2. In the Home Page, Under  **Apex Builder** , click on **Import**

  ![App Builder](images/apex_task3_step1.png "App Builder > Import ")


3. Select the updated file **WCC_RFP_Rest_Catalog_<your_wcc_hostname>.sql** ( eg: *WCC_RFP_Rest_Catalog_wccrfpmgmtdemo.sql* ) , ensure that the **File Type** is selected as **REST Source Catalog** and click **Next** Button

  ![REST Datasource sql file import](images/apex_task4_step2.png "WCC RFP Management APEX Application - REST Datasource Catalog Import Page")

4. Click **Next** in the **Import** Page

  ![REST Datasource Import](images/apex_task4_step3.png "WCC RFP Management APEX Application - REST Datasource Import Page")

5. In the **Rest Catalog Import** Page, Enter the value for **Catalog Group** and click on **Import REST Catalog** Button

 * **Catalog Group** : Enter
    ```
    <copy>WCC_RFP_REST_CATALOG_GROUP</copy>
    ```

  ![Rest Catalog Import](images/apex_task4_step4.png "WCC RFP Management APEX Application - Rest Catalog Import")


5. After the REST Catalog is imported, click on **1Services** under the **Contents** tab for the imported **WCC RFP Rest Catalog**

  ![Rest Catalog Imported](images/apex_task4_step5.png "WCC RFP Management APEX Application - Rest Catalog Imported")

6. In the **Catalog Services** list, click on the *Name* **quick\_search\_library**

  ![Catalog Services](images/apex_task4_step6.png "WCC RFP Management APEX Application - Catalog Services")

7. In the **Service Details** Section, Verify the **Base URL** with the URL for the WCC Instance Provisioned in the **Lab 3 - Initialize Environment** and click **Apply Changes** Button

  ![Service Details - Base URL Update](images/apex_task4_step7.png "WCC RFP Management APEX Application - Service Details - Base URL Update")


## Summary
You have now learned how to navigate the significant components of Oracle APEX and install and run a packaged application. You are now ready to **proceed to the next lab**.


## Acknowledgements

* **Authors-** Senthilkumar Chinnappa, Senior Principal Solution Engineer, Oracle WebCenter Content
* **Contributors-** Senthilkumar Chinnappa, Mandar Tengse , Parikshit Khisty
* **Last Updated By/Date-** Senthilkumar Chinnappa, July 2024
