# Create New RFP Document

## Introduction

In this lab, you will learn about the steps needed to Upload New RFP Document in the RFP Management System and also, select the relevant sections for the RFP Response. The System will automatically select the relevant section document template, and assigns/uploads against this newly uploaded RFP Document. For each of these Section Document, gets into the workflow, for further processing.

  ![Lab Flow](./images/create_new_rfp_doc_flow.png "Create New RFP Document - Lab Flow")

*Estimated Time*: 5 minutes

### Objectives

In this lab, you will:

* Navigate through the RFP Management Application
* Upload New RFP document
* Provide property information values for the RFP Document
* Select Sections
* Verify the Section documents is present in the Workflow in WCC

### Prerequisites
This lab assumes you have:
- A  Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup ( *Paid Tenants* only)
    - Lab: WCC Environment Setup
    - Lab: Initialize Environment
    - Lab: Setup Apex Application

## Task 1: Login to the RFP Management System Application

1. Log in to WebCenter Content Server.

2. Click **Browse Content** then **Retention Schedules**

3. On the Exploring Retention Schedule page, choose **Create** and then **Create Retention Category** on the page menu. On the Create or Edit Retention Category page, enter the details as shown in the image below.

    ![This image shows how to create retention category](./images/create-retention-category.png "Create Retention Category")
    ![Fill in the details on the Retention Category Create a page as shown in this image.](./images/category-create-form.png "Create Retention Category Page")

4. Click **Create**. Click on **Legal Documents** that is created under **Browse Content**.

5. In the Legal Documents Retention Category Page, click on **Create Records Folder** and create the *MOU* records folder as shown below
     ![Select the options listed in this image to create a Record Folder](./images/create-record-folder.png " Create Record Folder")

6. Fill in the details as shown in the below image and click on the **Create** button. Similarly, create the other two records folders i.e *Non-disclosure Agreement* records folder to store Non-disclosure agreement records and the *Software Agreement* Records Folder to store Software Agreement Records.
      !["Fill in the details on the Record Folder Create Page as shown in this image](./images/record-folder-createform.png "Create Record Folder Form")

7. After creating the 3 record folders, you must see the record folders in the **Legal Documents** category as shown below.
      ![Summary of the record folders after creation.](./images/record-folders-legal-doc-category.png "Record Folders in Legal Document Category")

## Task 2: Upload New RFP Document with properties and sections

1. In the row for the Legal Documents retention category on the Exploring Retention Schedule page, choose **Edit** then **Edit Disposition** from the item's Actions menu.
    ![Select the option shown in the image to add the disposition rule for the Legal Document Retention Category](./images/edit-disposition.png "Edit Disposition Rule on the Retention Category **Legal Documents** ")

2. In the Disposition Instructions area, click **Add**.

    > **Note:** The Category.Create right is required to perform this action. This right is assigned by default to the Records Administrator role.

   ![This image shows how disposition rule creation form.](./images/add-dispostition.png "Add Disposition Page")

3. On the Disposition Rule page, choose the disposition rule's triggering event from the Triggering Event (After) list. If the disposition rule has a retention period, enter an integer value for Retention Period (Wait for) and select the corresponding period from the Retention Period list. Select an action for the rule from the Disposition Action (Do) list.

4. Disposition rule for MOU records is 'When the MOUs are obsolete, delete all the revisions from the server'. In the **After** list select *Obsolete* event and choose *0 weeks* for the **Wait for** field. In the **Do** list select the *Delete All Revisions (Destroy Metadata)* action as shown in the image below.

5. In the **Notification Reviewer**, select the user *weblogic* who will be notified. In the **Advanced options** select the Records Folder for the disposition rule to be applied.

    ![Fill in the details as shown in this image to edit the disposition rule for the Legal Document category.](./images/dispostion-rule-creation-form.png  "Create Disposition Rule Page")

6. Click on **Submit Update** to apply changes to the MOU Record Folder. Click Ok.
    ![Click on Submit Update to apply the disposition rule on the MOU Record Folder.](./images/submit-update.png "Submit Update page ")

## Task 3: Verify the Section documents in WCC Workflow


 You may now **proceed to the next lab**.

## Learn More

* [Defining and Processing Dispositions](https://docs.oracle.com/en/middleware/webcenter/content/12.2.1.4/webcenter-content-manage/defining-and-processing-dispositions.html#GUID-0827B335-BA5E-4B9C-9270-27BE4520391C)

## Acknowledgements

* **Authors-** Shriraksha S Nataraj, Staff Solution Engineer, Oracle WebCenter Content
* **Contributors-** Shriraksha S Nataraj
* **Last Updated By/Date-** Shriraksha S Nataraj, August 2022
