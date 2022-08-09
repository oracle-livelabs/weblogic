# Introduction

## About this Workshop

 This workshop will help organizations kickstart their records management journey and help them to focus on the preservation of content for historical, legal, or archival purposes. It will also guide organizations to define, manage, and execute records and retention policies for all enterprise content from a single application. This workshop demonstrates how to dispose of obsolete content items, content items that are no longer needed by applying different types of disposition rules on the content using Oracle WebCenter Content Records Management.

*Estimated Time:* 3 hours

### About WebCenter Content Records Management

Oracle WebCenter Content provides unified records management capability across all the high­value information stored within it, including website content, electronic documents, digital assets, and images. This enables Oracle WebCenter Content to uniquely deliver a complete end-to-end system for document lifecycle management – from creation or capture to revision to archive and disposition. Oracle WebCenter Content Records Management system lets you retain and dispose of Organization's content by applying disposition or retention policies on the record. Not only must content be maintained, but it must also be defensibly disposed of once its usefulness has expired. Oracle WebCenter Content enables both the retention and disposition of information, allowing organizations to define, manage, and execute records and retention policies for all enterprise content from a single application.

In this workshop, you will understand the different types of disposition rules that can be applied to the 3 different record folders shown in the diagram below. An organization has legal documents that need to be categorized and stored in separate folders. Depending on its usage, records that are no longer required, need to be purged from the system. WebCenter Content Records Management provides various predefined events, retention periods, and actions that can be used according to the requirements.
    ![Workshop Architecture](./images/workshop-architecture.png "Workshop Architecture")

The Retention Category named **Legal Documents** contains 3 record folders: **MOU's**, **Non-disclosure Agreements**, and **Software Development Agreements**, each containing legal records. An *event-based* disposition rule is applied to the **MOU** Record Folder, where based on the occurrence of the event, the record gets closed or cut off and goes through an approval process before getting purged from the system. For the **Non-disclosure Agreement Record Folder**, the *time-based disposition* rule acts on the agreements. Based on a certain time period defined by the user, the agreement gets archived or removed from the system. Finally, an *event-time-based* disposition rule is applied to the **Software Development Agreement** record folder, which occurs when both an event and a time period defined by the user occur. After the records in each specific record folder have met the condition and been retained for a certain time period, they are then purged from the system after receiving approval from the authorized user based on the configuration.

### Objectives

In this lab, you will:

* Understand WebCenter Content Records Management
* Understand Retention Category and Disposition Rules
* Create Disposition rules on records

### Prerequisites

This lab assumes you have:

* A Free Tier, Paid or LiveLabs Oracle Cloud account

You may now **proceed to the next lab**.

## Learn More

* [Introduction To WebCenter Records](https://docs.oracle.com/en/middleware/webcenter/content/12.2.1.4/index.html)

## Acknowledgements

* **Authors-** Shriraksha S Nataraj, Staff Solution Engineer, Oracle WebCenter Content
* **Contributors-** Shriraksha S Nataraj
* **Last Updated By/Date-** Shriraksha S Nataraj, August 2022
