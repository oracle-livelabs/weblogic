# Verify Security Privilege on the Folders and Files

## Introduction

This lab will show you how to validate different Security Privileges set on folders and documents.

**Estimated Lab Time**: *30 minutes*

### Objectives

- Validate Security group, Accounts and ACLs set on Folders and Documents.

### Prerequisites

This lab assumes you have:

- Access to WCC Marketplace Environment

This lab assumes you have completed:

- Lab: Initialize WCC Environment
- Lab: Create Users and Groups
- Lab: Create Security Groups, Roles, Aliases and Accounts
- Lab: Create Folders and Files and set Different Security Permissions

## Task 1: Verify folder access set by Security Group with RWDA permission

1. Login to WCC RedwoodUI as HRAdmin/Welcome1 and navigate to **root** > **HRDocs** folder
2. Verify you can see icon to create folder and upload document
![This image shows the WCC HRDocs Folder](./images/hradmin-folder.png "WCC Instance HRDocs Folder")
3. Verify you can create a new folder and upload a new document
4. Click on checkbox to select the folder **HRAdmin Child Folder - Delete1** folder
5. Click **Delete** menu and delete the folder
![This image shows the WCC HRDocs Delete Folder](./images/hradmin-delete.png "WCC Instance HRDocs Delete Folder")

## Task 2: Verify folder access set by Security Group with only R and RWD permission

1. Login to WCC RedwoodUI as HRRep1/Welcome1 and navigate to **root** > **HRDocs** folder
2. Verify you don't see icons to create folder and upload document
![This image shows the WCC HRRep Folder](./images/hrrep-root-folder.png "WCC Instance HRRep Folder")
3. Click on checkbox to select the folder **HRAdmin Child Folder - Delete2** folder
4. Verify you don't see **Delete** menu
![This image shows the WCC HRRep delete Folder](./images/hrrep-root-menu.png "WCC Instance HRRep delete Folder")
5. Navigate to **HR Representatives Docs** folder
6. Verify you can see icon to create folder and upload document
![This image shows the WCC HRRep Root Folder](./images/hrrep-child-folder.png "WCC Instance HRRep Root Folder")
7. Verify you can create a new folder and upload a new document
8. Click on checkbox to select the folder **HRRep Child Folder - Delete1** folder
![This image shows the WCC HRRep Delete Folder Menu](./images/hrrep-child-menu.png "WCC Instance HRRep delete Folder Menu")
9. Click **Delete** menu and delete the folder
![This image shows the WCC HRRep Delete Folder Deleted](./images/hrrep-folder-deleted.png "WCC Instance HRRep delete Folder Deleted")

## Task 3: Verify folder access for the users not in security group

1. Login to WCC RedwoodUI as FinRep1/Welcome1 and navigate to **root** folder
2. Verify you don't see **HRDocs** folder
![This image shows the WCC FinRep Delete Folder](./images/finrep-root.png "WCC Instance FinRep Folder")

## Task 4: Verify folder access set by Account (User added to @Training\_R group in weblogic/IDCS)

1. Login to WCC RedwoodUI as TrainingRep1/Welcome1 and navigate to **root** > **HRDocs** > **Training Docs** folder
2. Verify you don't see icons to create folder and upload document
![This image shows the WCC TrainingRep1 Folder](./images/trainingrep1-training-docs-folder.png "WCC Instance TrainingRep1 Folder")
3. Click on checkbox to select the folder **TrainDoc Child Folder - Delete1** folder
4. Verify you don't see **Delete** menu
![This image shows the WCC TrainingRep1 Menu](./images/trainingrep1-training-doc-delete.png "WCC Instance TrainingRep1 Menu")

## Task 5: Verify folder access set by Account (User added to @Training\_RW group in weblogic/IDCS)

1. Login to WCC RedwoodUI as TrainingRep2/Welcome1 and navigate to **root** > **HRDocs** > **Training Docs** folder
2. Verify you can see icon to create folder and upload document
![This image shows the WCC TrainingRep2 Folder](./images/trainingrep2-folder.png "WCC Instance TrainingRep2 Folder")
3. Verify you can create a new folder and upload a new document
4. Click on checkbox to select the folder **TrainDoc Child Folder - Delete1** folder
5. Verify you don't see **Delete** menu
![This image shows the WCC TrainingRep2 Menu](./images/trainingrep2-delete.png "WCC Instance TrainingRep2 Menu")

## Task 6: Verify folder access set by Account (User added to @Training\_RWD group in weblogic/IDCS)

1. Login to WCC RedwoodUI as TrainingRep3/Welcome1 and navigate to **root** > **HRDocs** > **Training Docs** folder
2. Verify you can see icon to create folder and upload document
![This image shows the WCC TrainingRep2 Folder](./images/trainingrep2-folder.png "WCC Instance TrainingRep2 Folder")
3. Verify you can create a new folder and upload a new document
4. Click on checkbox to select the folder **TrainDoc Child Folder - Delete1** folder
5. Click **Delete** menu and delete the folder
![This image shows the WCC TrainingRep3 Menu](./images/trainingrep3-delete-folder.png "WCC Instance TrainingRep3 Menu")

## Task 7: Verify folder access set by Account (User added to @Training\_RWDA group in weblogic/IDCS)

1. Login to WCC RedwoodUI as TrainingAdmin/Welcome1 and navigate to **root** > **HRDocs** > **Training Docs** folder
2. Verify you can see icon to create folder and upload document
![This image shows the WCC TrainingRep2 Folder](./images/trainingrep2-folder.png "WCC Instance TrainingRep2 Folder")
3. Verify you can create a new folder and upload a new document
4. Click on checkbox to select the folder **TrainDoc Child Folder - Delete2** folder
5. Click **Delete** menu and delete the folder
![This image shows the WCC TrainingAdmin Folder](./images/trainingadmin-delete.png "WCC Instance TrainingAdmin Folder")

## Task 8: Verify folder access set by Account (User not added to any of Training\_ groups in weblogic/IDCS)

1. Login to WCC RedwoodUI as TrainingRep4/Welcome1 and navigate to **root** > **HRDocs** folder
2. Verify you cant see **Training Docs** folder
![This image shows the WCC TrainingRep4 Folder](./images/trainingrep4-user.png "WCC Instance TrainingRep4 Folder")

## Task 9: Verify folder access set by User Access List

1. Login to WCC RedwoodUI as TrainingRep1/Welcome1 and navigate to **root** > **HRDocs** > **Training Representative1 Docs** folder
2. Verify you can see icon to create folder and upload document
![This image shows the WCC TrainingRep1 Folder](./images/trainingrep1-folder.png "WCC Instance TrainingRep1 Folder")
3. Verify you can create a new folder and upload a new document
4. Click on checkbox to select the folder **TrainRep1 Child Folder - Delete1** folder
5. Click **Delete** menu and delete the folder
![This image shows the WCC TrainingRep1 Delete Folder](./images/trainingrep1-delete.png "WCC Instance TrainingRep1 Delete Folder")

## Task 10: Verify folder access set by Group Access List

1. Login to WCC RedwoodUI as TrainingRep1/Welcome1 and navigate to **root** > **HRDocs** > **Training Representatives Docs** folder
2. Verify you can see icon to create folder and upload document
![This image shows the WCC TrainingRep1 Group ACL Folder View](./images/trainingrep1-folder-groupacl.png "WCC Instance TrainingRep1 Group ACL Folder View")
3. Verify you can create a new folder and upload a new document
4. Click on checkbox to select the folder **TrainReps Child Folder - Delete1** folder
5. Verify you don't see **Delete** menu
![This image shows the WCC TrainingRep1 Group ACL Folder Delete](./images/trainingrep1-folder-delete-groupacl.png "WCC Instance TrainingRep1 Group ACL Folder Delete")

## Task 11: Verify folder access set by Role Access List

1. Login to WCC RedwoodUI as TrainingAdmin/Welcome1 and navigate to **root** > **HRDocs** > **HR Representatives1 Docs** folder
2. Verify you can't see icon to create folder and upload document
![This image shows the WCC TrainingAdmin Folder](./images/tainingadmin-folder.png "WCC Instance TrainingAdmin Folder")
3. Click on checkbox to select the folder **HR Representatives1 Child Folder - Delete1** folder
4. Verify you don't see **Delete** menu
![This image shows the WCC TrainingAdmin Menu](./images/trainingadmin-delete.png "WCC Instance TrainingAdmin Menu")

## Task 12: Verify Document access set by different ACLs

1. Login to WCC RedwoodUI as HRRep1/Welcome1 and navigate to **root** > **HRDocs** folder
2. Select checkbox against the file uploaded in **Lab 4: Create Folders and Files and set Different Security Permissions** > **Task 10: Upload document and Set Access List**
3. Verify you don't see **Move**, **Copy**, **Check In**, **Check out**, **Rename** and **Delete** menu
![This image shows the WCC HRRep1 File Menu](./images/hrrep-file-menu.png "WCC Instance HRRep File Menu")
4. Login to WCC RedwoodUI as TrainingRep3/Welcome1 and navigate to **root** > **HRDocs** folder
5. Select checkbox against the file uploaded in **Lab 4: Create Folders and Files and set Different Security Permissions** > **Task 10: Upload document and Set Access List**
6. Verify you can see **Move**, **Copy**, **Check In**, **Check out** and **Rename** menu
7. Verify you don't see **Delete** menu
![This image shows the WCC TrainingRep3 File Menu](./images/trainingrep3-delete-file.png "WCC Instance TrainingRep3 File Menu")
8. Login to WCC RedwoodUI as TrainingRep1/Welcome1 and navigate to **root** > **HRDocs** folder
9. Select checkbox against the file uploaded in **Lab 4: Create Folders and Files and set Different Security Permissions** > **Task 10: Upload document and Set Access List**
10. Click **Delete** menu and delete the file
![This image shows the WCC TrainingRep1 File Menu](./images/trainingrep1-training-doc-delete.png "WCC Instance TrainingRep1 File Menu")

This Completes this Live Lab.

### Learn More

- [Using Oracle WebCenter Content on Marketplace in Oracle Cloud Infrastructure](https://docs.oracle.com/en/cloud/paas/webcenter-content/webcenter-content-marketplace/index.html#provision-webcenter-content-stack)
- [Introduction To WebCenter Content](https://docs.oracle.com/en/middleware/webcenter/content/12.2.1.4/index.html)

## Acknowledgements

- **Authors-** Sujata Nayak, Consulting Member Technical Staff, Oracle WebCenter Content
- **Contributors-** Sujata Nayak, Senthilkumar Chinnappa, Mandar Tengse , Parikshit Khisty
- **Last Updated By/Date-** Sujata Nayak, December 2024
