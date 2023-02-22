# Event and Time-based disposition rule on Software Agreement Records

## Introduction

This lab showcases how to use both event and time as the criteria for the disposition rule to act upon the records. It shows you how to set up the disposition rule based on the event and time. It shows you how to check in a content item into the **Software Agreement** Record Folder and how the item is archived to a specific file location once the content has expired. The record goes through the workflow process and gets approved by the authorized user before getting expired.

*Estimated Time*: 30 minutes

### Objectives

In this lab, you will:

* Add Disposition Rule
* Check-In Content Item
* Pending Disposition Workflow
* Overview of Disposition Rules

### Prerequisites
This lab assumes you have:
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment
    - Lab: Event-based Disposition Rule on MOU Records (Task 1 is mandatory)
    - Lab: Time-based disposition Rule on Non-disclosure Agreement Records (Task 3 is mandatory)

## Task 1: Add Disposition Rule

1. Choose **Browse Content** then **Retention Schedules**. Select **Legal Documents** Retention Category and click on **Edit**.

2. Click on **Edit Disposition** and select **Add** to add the disposition rule. On the Disposition Rule page, select the  **Expired** for the **After** field. In the **Wait for** field, enter **6 months**.In the **Do** field, select **Archive** as shown in the image below.

3. In the **Advanced section**, select the record folder and enter the location where you want to archive the record as shown in the image below. Click **Ok**.
     ![Fill in the details as shown in this image to add the disposition rule for the Software Agreement Record Folder](./images/add-disposition-rule.png "Edit Disposition Rule")

## Task 2: Check-In Content Item to Software Agreement Record Folder

1. Click on **Create** and select **Create Content Item** as shown in the image below.
    ![This image shows to select the option to create a new content item in the record folder.](./images/checkin-new-content-item.png " Check-In Content Item")

2. Fill in the check-in form as shown below and for the **Primary File** field choose a file from the system.
    ![Fill in the details as shown in this image to check in a new content item in the Software Agreement Record Folder](./images/checkin-form.png "Check-In Form")

    ![Record after checking in to the Software Agreement Record Folder looks like this image shown.](./images/softwareagreementrecord.png "Software Agreement Record")

3. Click on the **i** icon on the Software Agreement Record which is recently checked in to view the content information, metadata information and the life cycle information of the record to see how the disposition rule has been applied to the Software Agreement record.
    ![Content Information Page of the Record](./images/record-content-info.png "Record Content Information")

    ![Disposition Rule that is applied on the Record item is seen in this image shown.](./images/content-life-cycle.png "Content Life Cycle Page")

4. To test the disposition rule and disposition action on the Software Agreement Record, enter an expiration date which is before 7 months old by selecting **Set Dates** and selecting **Expire** in the **Actions** menu of the content information page as shown below. The content item begins disposition processing based on the expired date. If you check the life cycle for the content item, you can see the dates are already set for processing.
   ![Select the options shown in this image to set an expiration date for the Software Agreement Record](./images/set-dates.png "Set Dates for the Record ")

5. Provide a valid reason for expiring the Software Agreement Record and select the expiration date which is 6 or 7 months old from the release date. This step is performed to test the disposition rule.

   ![Enter in a valid reason as shown below and select the expiration date which is 6 or 7 months old date from the release date of the Software Agreement Record](./images/expire-reason.png "Expire Reason and Expire Date Page")

6. After you perform this step, you can see that the disposition processing has taken place and the Software Agreement Record is expired and is depicted by a scratch on the title of the Record in the Record Folder page as shown below.

   ![Record is expired as shown in this image.](./images/record-cut-off.png "Record Expired")

## Task 3: Pending Disposition Workflow

1. Now that the disposition rule is processed, it goes through a workflow process before the disposition action acts on the Record. As we just created the user in the previous lab, log in as *Mark* to the content server.

> **Note:** Pending events and review cycles are processed by the system every night on a 24-hour cycle. Notifications are sent daily at midnight. Use the **Batch Services** options on the Records menu to process certain actions immediately rather than wait for the scheduled processing time. Options on the Batch menu include as shown in the image below. Select **Run All** or you can run individual options too such as **Process Dispositions** and **Process Reviews**. By performing this step, the user gets notified of the Pending Approvals.
   ![Run batch services to get notified of the Pending Approval Notification](./images/run-batch-services.png "Run Batch Services Option")

2. To check the Pending Approvals for Disposition, Click on **My Content Server** and select **My Records Assignments**. After running the batch services, it directly takes the user to the approval page.
    ![Select My Records Assignments highlighted in the rectangular box to check the pending disposition approvals](./images/pending-approvals.png "Pending Approval Page")

    Another way to see the Pending Approvals is by selecting the **Records** menu and clicking on **Approvals** and then selecting either **Pending Dispositions** or **Pending Reviews**.
     ![This image shows another alternative to check the Pending Disposition Approvals](./images/pending-approval-another-way.png "Pending Approval Page through Records Option")

3. Select the record item from the Pending Approval Page and click on **Approve**. Provide a valid reason and click on **Ok**.
   ![Reason for Approval](./images/reason-for-approval.png "Reason For Approval")

4. Since the Disposition Action is **Archive** it goes through 2 steps of Approval one approval is for the archival and another approval is for the completion of the Disposition Action. Click on **Approve** and give a valid reason. Run the batch service **Process Dispositions** to get the record for the completion approval step.
    ![Pending Approval for the Completion Step.](./images/pending-approval-2.png "Pending Approval")

    ![Reason for the Approval for the Completion Step.](./images/reason-approval-2.png "Reason For Approval")

5. After the approval process is complete, the record gets disposed of from the content server and gets stored in the file location specified in the disposition rule.
    > **Note:** Run the batch services again and wait for some time for the disposition processing.
    ![Record is no longer present in the Software Agreement Record Folder.](./images/record-disposed.png "Record Purged from the system")

    ![Record is archived in the file location specified as shown in the image below.](./images/archived-in-folder.png "Archived Record Item")

## Task 4: Overview of Disposition Rules on Legal Document Category

  The image below shows the disposition rules applied to different record folders which we created in previous labs. It also shows the steps that are completed and the reviewer's name along with the Record Folder name. Three different types of disposition rule i.e **event-based**, **time-based** and **event-time based** disposition rules are applied on 3 different record folders which are *MOUs*, *Non-disclosure Agreement* and *Software Document Agreement* record folders respectively.
    ![Three different types of disposition rules acted on three different record folders under the same Retention Category. The image shows the overview of the disposition rules.](./images/overview-of-entire-disposition-rule.png "Disposition Rules")

You may now **proceed to the next lab**.

## Learn More

* [Defining and Processing Dispositions](https://docs.oracle.com/en/middleware/webcenter/content/12.2.1.4/webcenter-content-manage/defining-and-processing-dispositions.html#GUID-0827B335-BA5E-4B9C-9270-27BE4520391C)

## Acknowledgements

* **Author-**  Shriraksha S Nataraj, Staff Solution Engineer, Oracle WebCenter Content
* **Contributors-** Shriraksha S Nataraj
* **Last Updated By/Date-** Shriraksha S Nataraj, August 2022
