# Setup RFP Management APEX Application

## Introduction

In this lab, you learn to install and run Oracle APEX Application for RFP Management System.

This lab also covers updating the APEX Rest Datasource urls & credentials for connecting to WebCenter Content Instance

**Estimated Lab Time**: *20 minutes*

### Objectives

In this lab, you will:

- Navigate through Oracle APEX
- Create New Workspace
- Login to Workspace and Install Packaged Application.
- Update Rest Data sources URL and credentials

### Prerequisites

This lab assumes you have:

- A  Paid or LiveLabs Oracle Cloud account
- You have completed:
  - Lab: Prepare Setup ( *Paid Tenants* only)
  - Lab: Setup WCC Marketplace Environment
  - Lab: Initialize Environment

## Task 1: Create New APEX Workspace for RFP Management Application

To create new APEX workspace, you need log in to Oracle APEX's default **INTERNAL** Workspaces as **ADMIN** User (or) the user with Administrator Privilege on the APEX Instance

1. On the new *web browser* window , Login to the APEX/ORDS URL as **ADMIN** User of System's **INTERNAL** Workspace. Details are provided below
    - **URL**
          ```
          <copy>http://localhost:16200/ords/</copy>
          ```

         > Note : Replace `"http://localhost"` with your **hosturl** ( eg: `"http://wcc-rfpmgmt-livelab.livelabs.oraclevcn.com"` or `"https://192.0.0.0""`)
    - **Workspace Name**
          ```
          <copy>INTERNAL</copy>
          ```
    - **Username**
          ```
          <copy>ADMIN</copy>
          ```
    - **Password**
          ```
          <copy>WelCwcm123##</copy>
          ```
    > **For ATP DB** *, ADMIN password is same as the ADMIN DB schema user password*.
    > *If any issues with ADMIN credentials, Refer to **Appendix 4: Reset ADMIN password for APEX/ORDS** of the previous lab **Initialize WCC Environment** to reset ADMIN Password*
  ![This image shows the APEX/ORDS Login Page](./images/apex_login_internal.png "APEX/ORDS Login Page")

2. In the *Administration Services* Landing page , Click on **Create Workspace** button on the top right corner
  ![This image shows the APEX/ORDS Landing Page](./images/apex_create_workspace_homepage.png "APEX/ORDS Landing Page")

3. Provide the value for **Workspace Name**  and click **Next** Button
        ```
        <copy>WCCRFPMGMT</copy>
        ```
  ![This image shows the APEX/ORDS Create Workspace Page](./images/apex_create_workspace_step1.png "APEX/ORDS Create Workspace Page")

4. Provide the values for DB Schema details as mentioned below and click **Next** Button
    - **Re-use existing schema?**: Select **No**
    - **Schema Name**: Enter
          ```
          <copy>WCCRFPMGMT_SCHEMA</copy>
          ```
    - **Schema Password**: Enter
          ```
          <copy>WelCwcm123##</copy>
          ```
    - **Space Quota (MB)**: Select **500**
  ![This image shows the APEX/ORDS Create Workspace Page - DB Schema Details](./images/apex_create_workspace_step2.png "APEX/ORDS Create Workspace Page - DB Schema Details")

5. Provide the values for Workspace **ADMIN** User details as mentioned below and click **Next** Button

    - **Administrator Username**: Enter
          ```
          <copy>ADMIN</copy>
          ```
    - **Administrator Password**: Enter
          ```
          <copy>Welcome1</copy>
          ```
    - **First Name**: Enter
          ```
          <copy>Admin</copy>
          ```
    - **Last Name**: Enter
          ```
          <copy>User</copy>
          ```
    - **Email**: Enter your email id
          ```
          <copy>admin_user@email.com</copy>
          ```
  ![This image shows the APEX/ORDS Create Workspace Page - Admin User Details](./images/apex_create_workspace_step3.png "APEX/ORDS Create Workspace Page - ADMIN User Details")

6. Review the details and click **Create Workspace** Button
 ![This image shows the APEX/ORDS Create Workspace Page](./images/apex_create_workspace_step4.png "APEX/ORDS Create Workspace Page")

7. After the workspace is successfully created, it will display  workspace details.  click **Done** Button

 ![This image shows the APEX/ORDS Workspace Created Page](./images/apex_create_workspace_step5.png "APEX/ORDS Workspace Created Page")

## Task 2: Login to Newly Created APEX Workspace

To log in to Oracle APEX, you need a Workspace Name, username, and the password created for that Workspace. In this hands-on lab, you log in to your Oracle APEX Workspace.

1. To login to your Oracle APEX Workspace, perform the following steps:
    - Open your browser and enter the **URL** to sign in to the APEX development environment.
      - **URL**
            ```
            <copy>http://localhost:16200/ords/</copy>
            ```

            > Note : Replace `"http://localhost"` with your **hosturl** ( eg: `"http://wcc-rfpmgmt-livelab.livelabs.oraclevcn.com"` or `"https://192.0.0.0"`)

    - The login page appears. Enter the **Workspace Name, Username, and Password**. Click **Sign In**.
      - **Workspace Name**: Enter
            ```
            <copy>WCCRFPMGMT</copy>
            ```
      - **Username**: Enter
            ```
            <copy>ADMIN</copy>
            ```
      - **Password**: Enter
            ```
            <copy>Welcome1</copy>
            ```
  ![Workspace Login](./images/apex_login_workspace_step1.png "Login to APEX Workspace")

2. If its first time Login, Change password for the ADMIN user. You can provide the same Password value and click on **Change Password**.
    > Skip this step if it does not prompt for Change Password

    - **New Password**: Enter
          ```
          <copy>Welcome1</copy>
          ```
    - **Confirm Password**: Enter
          ```
          <copy>Welcome1</copy>
          ```
  ![Reset Password on First Login Page](./images/apex_login_workspace_step2.png "Reset Password on First Login")

3. The Workspace home page appears.

  ![Workspace Home Page](./images/apex_login_workspace_step3.png "Workspace Home Page")

## Task 3: Install RFP Management Application

This task covers installing and running a WCC RFP Management System APEX application.

1. Edit the downloaded APEX Application sql file **wcc-rfp-mgmt-system-apex-app.sql** in a text editor (eg: Notepad) , replace `"http://localhost"` with your **hosturl** ( eg: `"http://wcc-rfpmgmt-livelab.livelabs.oraclevcn.com"` or `"https://192.0.0.0"`) and save the file.
  ![Edit in Notepad](./images/apex_task3_step0_1.png "replace localhost with <your_wcc_hostname> ")

2. After Login to the WORKSPACE **WCCRFPMGMT** as ADMIN user, in the Home Page, Under  **Apex Builder** , click on **Import**
  ![App Builder](./images/apex_task3_step1.png "App Builder > Import ")

3. Select the updated file **wcc-rfp-mgmt-system-apex-app.sql**  , ensure that the **File Type** is selected as **Application, Page or Component** and click **Next** Button
  ![Application sql file import](./images/apex_task3_step2.png "WCC RFP Management APEX Application Import Page")

4. In the **Install Application** Page, Verify the below values and click **Install Application** Button

    - *Current Workspace* : **WCCRFPMGMT**
    - *Parsing Schema* : **WCCRFPMGMT_SCHEMA**
    - *Build Status* : **Run and Build Application**
    - *Install as Application* : **Auto Assign New Application ID**
  ![Install Application Page](./images/apex_task3_step3.png "WCC RFP Management APEX  - Install Application Page")

5. In the **Install Application** - **Credentials** Page, for **Credentials for WCC RFP Mgmt**, Update the values for the below and click **Next** Button
    - **Client ID or Username** : Enter
          ```
          <copy>weblogic</copy>
          ```
    - **Client Secret or Password** : Enter
          ```
          <copy>Welcome1</copy>
          ```
    - **Verify Client Secret / Password** : Enter
          ```
          <copy>Welcome1</copy>
          ```
  ![Install Application - Credentials Page](./images/apex_task3_step4.png "WCC RFP Management APEX  - Install Application - Credentials Page")

6. After the Credentials is updated, in the **Application Installed** Page, click on **Install Supporting Objects** button
  ![Application Installed - Install Supporting Objects](./images/apex_task3_step5.png "WCC RFP Management APEX  - Application Installed - Install Supporting Objects")

7. After the Supporting Objects installed, click on **Install Summary** button , to view the status of the Supporting objects installation
  ![Supporting Objects Installed](./images/apex_task3_step6.png "WCC RFP Management APEX Application - Supporting Objects Installed")

## Task 4: Import REST DataSource Catalog

This task covers importing and configuring Rest Datasource Catalog.

1. Edit the downloaded APEX Application sql file **WCC\_RFP\_Rest\_Catalog.sql** in a text editor (eg: Notepad) , replace `"http://localhost"` with your **hosturl** ( eg: `"http://wcc-rfpmgmt-livelab.livelabs.oraclevcn.com"` or `"https://192.0.0.0"`)  and save the file.
  ![Edit in Notepad](./images/apex_task4_step0_1.png "replace localhost with <your_wcc_hostname> ")

2. In the Home Page, Under  **Apex Builder** , click on **Import**
  ![App Builder](./images/apex_task3_step1.png "App Builder > Import ")

3. Select the updated file **WCC_RFP_Rest_Catalog.sql** , ensure that the **File Type** is selected as **REST Source Catalog** and click **Next** Button
  ![REST Datasource sql file import](./images/apex_task4_step2.png "WCC RFP Management APEX Application - REST Datasource Catalog Import Page")

4. Click **Next** in the **Import** Page
  ![REST Datasource Import](./images/apex_task4_step3.png "WCC RFP Management APEX Application - REST Datasource Import Page")

5. In the **Rest Catalog Import** Page, Enter the value for **Catalog Group** and click on **Import REST Catalog** Button
    - **Catalog Group** : Enter
            ```
            <copy>WCC_RFP_REST_CATALOG_GROUP</copy>
            ```
  ![Rest Catalog Import](./images/apex_task4_step4.png "WCC RFP Management APEX Application - Rest Catalog Import")

6. After the REST Catalog is imported, click on **1Services** under the **Contents** tab for the imported **WCC RFP Rest Catalog**
  ![Rest Catalog Imported](./images/apex_task4_step5.png "WCC RFP Management APEX Application - Rest Catalog Imported")

7. In the **Catalog Services** list, click on the *Name* **quick\_search\_library**
  ![Catalog Services](./images/apex_task4_step6.png "WCC RFP Management APEX Application - Catalog Services")

8. In the **Service Details** Section, Verify the **Base URL** with the URL for the WCC Instance Provisioned in the **Lab 3 - Initialize Environment** and click **Apply Changes** Button
  ![Service Details - Base URL Update](./images/apex_task4_step7.png "WCC RFP Management APEX Application - Service Details - Base URL Update")

## Task 5 : Grant connect for ACL

Login to the Database as **sys** or user with **sysdba** privileges and perform the below steps

1. Find the latest version schema name
            ```
            SQL> SELECT  schema  FROM dba_registry WHERE comp_id = 'APEX' ORDER BY schema DESC FETCH FIRST 1 ROW ONLY;
            ```

2. Update the password and unlock the ADMIN User

            ```
            <copy>
            BEGIN
            DBMS_NETWORK_ACL_ADMIN.APPEND_HOST_ACE(
                  host => '*',
                  ace => xs$ace_type(privilege_list => xs$name_list('connect', 'resolve'),
                        principal_name => 'APEX_230200',
                        principal_type => xs_acl.ptype_db
                  )
            );
            END;
            /
            </copy>
            ```

      > Note : Replace `"APEX_230200"` with your **schema** retrieved from the above select query

## Task 6 : Add Users in APEX

1. Login to your Oracle APEX Workspace, using the following steps:

    - Open your browser and enter the **URL** to sign in to the APEX development environment.
      - URL
            ```
            <copy>http://localhost:16200/ords/</copy>
            ```

           > Note : Replace `"http://localhost"` with your **hosturl** ( eg: `"http://wcc-rfpmgmt-livelab.livelabs.oraclevcn.com"` or `"https://192.0.0.0""`)

    - The login page appears. Enter the **Workspace Name, Username, and Password**. Click **Sign In**.
      - **Workspace Name**: Enter
            ```
            <copy>WCCRFPMGMT</copy>
            ```
      - **Username**: Enter
            ```
            <copy>ADMIN</copy>
            ```
      - **Password**: Enter
            ```
            <copy>Welcome1</copy>
            ```
  ![Workspace Login](./images/apex_login_workspace_step1.png "Login to APEX Workspace")

2. Click on the *User Setting* icon next to the User name and click on **Manage Users and Groups**
  ![Manage Users and Groups](./images/add_apex_users_step2.png "Manage Users and Groups")

3. Check if the Users are already present. If not, create the users by clicking on **Create User** button
  ![Create User](./images/add_apex_users_step3.png "Create User")

4. In the **Create User** Page, provide the below values for creating the user **SALES_REP** and click **Create User** button

    - **Username**: Specify
          ```
          <copy>SALES_REP</copy>
          ```
    - **Email Address**: Specify your email address. eg:
          ```
          <copy>sales_rep@email.com</copy>
          ```
    - **First Name**: Specify
          ```
          <copy>Sales</copy>
          ```
    - **Last Name**: Specify
          ```
          <copy>Representative</copy>
          ```
    - **Password**: Specify
          ```
          <copy>Welcome1</copy>
          ```
    - **Confirm Password**: Specify
          ```
          <copy>Welcome1</copy>
          ```
    - **Require Change of Password on First Use** : *Disable/Un-Check*
  ![Create User - SALES_REP](./images/add_apex_users_step4.png "Create User - SALES_REP")

5. Similarly, create the other users as below:

      - **TECHNICAL_ARCHITECT** User
           - **Username**: Specify
                  ```
                  <copy>TECHNICAL_ARCHITECT</copy>
                  ```
           - **Email Address**: Specify your email address. eg:
                  ```
                  <copy>technical_architect@email.com</copy>
                  ```
           - **First Name**: Specify
                  ```
                  <copy>Technical</copy>
                  ```
           - **Last Name**: Specify
                  ```
                  <copy>Architect</copy>
                  ```
           - **Password**: Specify
                  ```
                  <copy>Welcome1</copy>
                  ```
           - **Confirm Password**: Specify
                  ```
                  <copy>Welcome1</copy>
                  ```
           - **Require Change of Password on First Use** : *Disable/Un-Check*

      - **FINANCE** User
           - **Username**: Specify
                  ```
                  <copy>FINANCE</copy>
                  ```
           - **Email Address**: Specify your email address. eg:
                  ```
                  <copy>finance@email.com</copy>
                  ```
           - **First Name**: Specify
                  ```
                  <copy>Finance</copy>
                  ```
           - **Last Name**: Specify
                  ```
                  <copy>Analyst</copy>
                  ```
           - **Password**: Specify
                  ```
                  <copy>Welcome1</copy>
                  ```
           - **Confirm Password**: Specify
                  ```
                  <copy>Welcome1</copy>
                  ```
           - **Require Change of Password on First Use** : *Disable/Un-Check*

      - **LEGAL** User
           - **Username**: Specify
                  ```
                  <copy>LEGAL</copy>
                  ```
           - **Email Address**: Specify your email address. eg:
                  ```
                  <copy>legal@email.com</copy>
                  ```
           - **First Name**: Specify
                  ```
                  <copy>Legal</copy>
                  ```
           - **Last Name**: Specify
                  ```
                  <copy>Advisor</copy>
                  ```
           - **Password**: Specify
                  ```
                  <copy>Welcome1</copy>
                  ```
           - **Confirm Password**: Specify
                  ```
                  <copy>Welcome1</copy>
                  ```
           - **Require Change of Password on First Use** : *Disable/Un-Check*

  ![Create Other Users](./images/add_apex_users_step5.png "Create Other Users")

## Task 7: Add Section Templates in RFP Response Management Application

1. To login to the WCC RFP Response Management System Application, perform the following steps:

    - Open your browser and enter the **URL** to sign in to the APEX development environment.
      - URL
            ```
            <copy>http://localhost:16200/ords/r/wccrfpmgmt/rfp-response-management-system/</copy>
            ```

           > Note : Replace `"http://localhost"` with your **hosturl** ( eg: `"http://wcc-rfpmgmt-livelab.livelabs.oraclevcn.com"` or `"https://192.0.0.0""`)

      - The login page appears. Enter the **Username, and Password**. Click **Sign In**.
        - **Username**: Enter
              ```
              <copy>ADMIN</copy>
              ```
        - **Password**: Enter
              ```
              <copy>Welcome1</copy>
              ```
  ![Application Login](./images/apex_setup_task5_step1.png "Login to APEX Application")

2. On the left navigation menu, click on **Sections** and click on **Create** button
  ![Navigate to Sections](./images/apex_setup_sections_task5_step2.png "Click on Sections")

3. In the **Manage Section Form** window, enter the below values and click on **Create** Button

    - **Name**: Specify
          ```
          <copy>Title and Summary</copy>
          ```
    - **Description**: Specify
          ```
          <copy>This is sample template for Title and Summary Section</copy>
          ```
    - **Template**: Browse and select the file **Title & summary.docx** from the downloaded **wcc\_rfp\_resources.zip** file ( in **Lab 1 - Prepare Setup**)
    - **Type**: Leave the default as **SECTION**
    - **Display Order**: Specify
          ```
          <copy>10</copy>
          ```
    - **Active**: Leave the default as **Y**
    - **Section Owner**: Specify
          ```
          <copy>Sales Rep</copy>
          ```
    - **Instructions**: Specify
          ```
          <copy>Update the Title and Summary section</copy>
          ```
    - **Expectation**: Specify
          ```
          <copy>Updated with relevant info</copy>
          ```
  ![Create Title and Summary Section](./images/apex_setup_sections_task5_step3.png "Create Title and Summary Section")
  ![Title and Summary Section Created](./images/apex_setup_sections_task5_step3.png "Title and Summary Section Created")

4. Similarly, create the below sections as well :

    - **Technical Design** Section
           - **Name**: Specify
                  ```
                  <copy>Technical Design</copy>
                  ```
           - **Description**: Specify
                  ```
                  <copy>This is template for Technical Design Section</copy>
                  ```
           - **Template**: Browse and select the file **Technical Design.docx** from the downloaded **wcc\_rfp\_resources.zip** file ( in **Lab 1 - Prepare Setup**)
           - **Type**: Leave the default as **SECTION**
           - **Display Order**: Specify
                  ```
                  <copy>20</copy>
                  ```
           - **Active**: Leave the default as **Y**
           - **Section Owner**: Specify
                  ```
                  <copy>Technical Architect</copy>
                  ```
           - **Instructions**: Specify
                  ```
                  <copy>Update the Technical Design section</copy>
                  ```
           - **Expectation**: Specify
                  ```
                  <copy>Updated with relevant info</copy>
                  ```
      ![Create Technical Design Section](./images/apex_setup_sections_task5_step4.png "Create Technical Design Section")
    - **Pricing And BOM** Section
           - **Name**: Specify
                  ```
                  <copy>Pricing And BOM</copy>
                  ```
           - **Description**: Specify
                  ```
                  <copy>This is template for Pricing And BOM Section</copy>
                  ```
           - **Template**: Browse and select the file **Finance.docx** from the downloaded **wcc\_rfp\_resources.zip** file ( in **Lab 1 - Prepare Setup**)
           - **Type**: Leave the default as **SECTION**
           - **Display Order**: Specify
                  ```
                  <copy>30</copy>
                  ```
           - **Active**: Leave the default as **Y**
           - **Section Owner**: Specify
                  ```
                  <copy>Finance</copy>
                  ```
           - **Instructions**: Specify
                  ```
                  <copy>Update the Pricing And BOM section</copy>
                  ```
           - **Expectation**: Specify
                  ```
                  <copy>Updated with relevant info</copy>
                  ```
      ![Create Pricing And BOM Section](./images/apex_setup_sections_task5_step4_2.png "Create Pricing And BOM Section")
    - **Legal** Section
           - **Name**: Specify
                  ```
                  <copy>Legal</copy>
                  ```
           - **Description**: Specify
                  ```
                  <copy>This is sample template for Legal Section</copy>
                  ```
           - **Template**: Browse and select the file **Legal_Template.docx** from the downloaded **wcc\_rfp\_resources.zip** file ( in **Lab 1 - Prepare Setup**)
           - **Type**: Leave the default as **SECTION**
           - **Display Order**: Specify
                  ```
                  <copy>40</copy>
                  ```
           - **Active**: Leave the default as **Y**
           - **Section Owner**: Specify
                  ```
                  <copy>Legal</copy>
                  ```
           - **Instructions**: Specify
                  ```
                  <copy>Update the Legal section</copy>
                  ```
           - **Expectation**: Specify
                  ```
                  <copy>Updated with relevant info</copy>
                  ```
      ![Create Legal Section](./images/apex_setup_sections_task5_step4_3.png "Create Legal Section")

5. This shows the summary of all the sections created.

  ![Section Summary](./images/apex_setup_sections_task5_step5.png "Summary of all the sections created")

    **Summary**

    You have now successfully setup the RFP Response Management Application for the RFP Application and User Flow.

You are now ready to **proceed to the next lab**.

## Appendix 1: Configure Wallet for https connectivity

   These steps are to be performed only if the secured http protocol is used by the WebCenter Content ( *ie URL has **https*** )
   > **Note:** *If the DB System was created with multi-nodes, the Steps 1.2 and 1.3 needs to be performed on all the DB Nodes created in the DB System*

- This consists of the below steps:
  - **Download certificate**
  - **Connect to DB System via SSH and create wallet**
  - **Configure APEX to use wallet directory**

### **1.1 Download Certificate**

   1. Open your browser and enter the **URL** to sign in to the APEX development environment.
      - URL
            ```
            <copy>http://localhost:16200/ords/</copy>
            ```

      > Note : Replace `"http://localhost"` with your **hosturl** ( eg: `"http://wcc-rfpmgmt-livelab.livelabs.oraclevcn.com"` or `"https://192.0.0.0""`)

   2. In the browser header section, before the url, click on the **Not Secure** icon. Then click on **Certificate is not valid** to **Show certificate** details
      > **Note** : If the url is configured with valid certificate , it'll show a **Secure Lock** icon and will list as **Certificate is valid**
      ![Open Certificate Info](/weblogic/webcenter-content/wcc-rfp-mgmt/04-setup-apex-application/images/apex_https_setup_ap1_step1_1_upt.png "View the Certificate details")

   3. In the **Certificate Viewer** window, in the **Details** tab, click on the top root entry under the **Certificate Hierarchy** and click **Export** button
      ![Export Certificate](/weblogic/webcenter-content/wcc-rfp-mgmt/04-setup-apex-application/images/apex_https_setup_ap1_step1_2_upt.png "View the Certificate details and export")

   4. Save the file as the below filename
      - **Filename**
            ```
            <copy>WCCRFPMGM.crt</copy>
            ```

      ![Save Certificate](/weblogic/webcenter-content/wcc-rfp-mgmt/04-setup-apex-application/images/apex_https_setup_ap1_step1_3_upt.png "Save the certificate as crt")

### **1.2 Connect to DB System via SSH and create wallet**

   1. Log in to **OCI Console**, navigate to **Oracle Database**, then to **Oracle Base Database Service** and Click on the DB System **wcc-rfpmgmt-DBSystem** ( *which was created as part of the Lab **Prepare Setup*** )
      ![Oracle DB System](/weblogic/webcenter-content/wcc-rfp-mgmt/04-setup-apex-application/images/apex_https_setup_ap1_step2_1_upt.png "View Oracle DB System details")

   2. Scroll down to the **Resources** Section and click on **Nodes**. Note the *IP Address* of all the Nodes listed
      ![Oracle DB System Nodes and IP Info](/weblogic/webcenter-content/wcc-rfp-mgmt/04-setup-apex-application/images/apex_https_setup_ap1_step2_2_upt.png "View Oracle DB System Node IP details")

   3. Open a terminal or a bash window , and invoke the below ssh command to login to the Node as **opc** user and then switch to **oracle** user
      - **ssh command**
            ```
            <copy>ssh -i db-ssh.key opc@xxx.xxx.xxx.xxx
            sudo su - oracle </copy>
            ```

      - **Note** :
        - **db-ssh.key** - is the key used/created while creating the DB System ( in Lab **Prepare Setup** , **Task 3: Create Database**, **3.2 Create a New DB System**). *FYI, Also, if **vault** was used for storing keys and secrets, this key can be obtained from there as well*
        - **xxx.xxx.xxx.xxx** - replace this value with the ip address of the node

      ![SSH to Node](/weblogic/webcenter-content/wcc-rfp-mgmt/04-setup-apex-application/images/apex_https_setup_ap1_step2_3_upt.png "SSH to Node")

   4. Open the previously downloaded **WCCRFPMGM.crt** certificate file in Notepad or Text Editor , and copy its contents.
      ![Copy Certificate contents](/weblogic/webcenter-content/wcc-rfp-mgmt/04-setup-apex-application/images/apex_https_setup_ap1_step2_4_upt.png "Copy Certificate contents")

   5. In the terminal window, invoke the below command to create file **/tmp/WCCRFPMGM.crt**, paste the certificate contents and save the crt file
      - **ssh command**
            ```
            <copy>WCCRFPMGM.crt/</copy>
            ```

      ![create certificate file in DB Node](/weblogic/webcenter-content/wcc-rfp-mgmt/04-setup-apex-application/images/apex_https_setup_ap1_step2_5_upt.png "create certificate file in DB Node temp directory")

   6. In the terminal window, invoke the below commands to create the wallet directory, create the wallet, and import the certificate as trusted certificate. Note down the **$ORACLE\_HOME/db\_wallet** location ( eg: **/u01/app/oracle/product/19.0.0.0/dbhome_1/db\_wallet**)
      - **ssh commands**
           - *Create wallet directory and create a oracle wallet in that directory ( Note: if this wallet directory and wallet files are already present, then skip this creation command)*
                  ```
                  <copy>
                        mkdir -pm 777 $ORACLE_HOME/db_wallet
                        $ORACLE_HOME/bin/orapki wallet create -wallet $ORACLE_HOME/db_wallet  -pwd WelCwcm123## -auto_login
                  </copy>
                  ```
           - *Invoke the below command to add the certificate to the trusted certificates list of the wallet*
                  ```
                  <copy>
                        $ORACLE_HOME/bin/orapki wallet add -wallet $ORACLE_HOME/db_wallet -trusted_cert -cert "/tmp/WCCRFPMGM.crt" -pwd WelCwcm123##
                  </copy>
                  ```
           - *Invoke these commands to list the certificates present in that wallet and also display the full path of the wallet directory (this directory is used for configuring **Wallet Path** in APEX)*
                  ```
                  <copy>
                        $ORACLE_HOME/bin/orapki wallet display -wallet $ORACLE_HOME/db_wallet  -pwd WelCwcm123##
                        echo
                        echo $ORACLE_HOME/db_wallet
                        ls -ltrh $ORACLE_HOME/db_wallet
                  </copy>
                  ```

      ![wallet creation in DB Node](/weblogic/webcenter-content/wcc-rfp-mgmt/04-setup-apex-application/images/apex_https_setup_ap1_step2_6_upt.png "wallet creation in DB Node and import certificate")

### **1.3 Configure APEX to use wallet directory**

      To Configure APEX to use wallet directory, you need log in to Oracle APEX's default **INTERNAL** Workspaces as **ADMIN** User (or) the user with Administrator Privilege on the APEX Instance

   1. On the new *web browser* window , Login to the APEX/ORDS URL as **ADMIN** User of System's **INTERNAL** Workspace. Details are provided below
      - **URL**
            ```
            <copy>http://localhost:16200/ords/</copy>
            ```

        > Note : Replace `"http://localhost"` with your **hosturl** ( eg: `"http://wcc-rfpmgmt-livelab.livelabs.oraclevcn.com"` or `"https://192.0.0.0""`)
      - **Workspace Name**
            ```
            <copy>INTERNAL</copy>
            ```
      - **Username**
            ```
            <copy>ADMIN</copy>
            ```
      - **Password**
            ```
            <copy>WelCwcm123##</copy>
            ```
   2. Navigate to **Manage Instance**, **Instance Settings**, click on **Wallet** tab , provide the below details and click on **Apply Changes** button
      - **Wallet Path**
            ```
            <copy>file:/u01/app/oracle/product/19.0.0.0/dbhome_1/db_wallet</copy>
            ```
      - **Auto-login Wallet** - *Un-Checked*
      - **Password**
            ```
            <copy>WelCwcm123##</copy>
            ```
      - **Confirm Password**
            ```
            <copy>WelCwcm123##</copy>
            ```
      - **Note** : *If you see any issue with the APEX URL, click on the link on error list and select the default url*

      ![wallet update in APEX](/weblogic/webcenter-content/wcc-rfp-mgmt/04-setup-apex-application/images/apex_https_setup_ap1_step3_2_upt.png "wallet update in APEX")

## Acknowledgements

- **Authors-** Senthilkumar Chinnappa, Senior Principal Solution Engineer, Oracle WebCenter Content
- **Contributors-** Senthilkumar Chinnappa, Mandar Tengse , Parikshit Khisty
- **Last Updated By/Date-** Senthilkumar Chinnappa, July 2024
