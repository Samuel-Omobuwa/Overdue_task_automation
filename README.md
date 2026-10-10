# Overdue Task Automation with Microsoft Power Automate

## Project Overview

Overdue Task Automation is a workflow built with Microsoft Power Automate to identify overdue tasks from an Excel tracker stored in OneDrive and notify the responsible owners by email.

The workflow reduces manual follow-up, improves visibility into outstanding actions, and promotes accountability by providing owners with a consolidated view of their overdue tasks.

## Problem Statement

Tracking overdue tasks manually can be time-consuming, particularly when multiple owners are responsible for several actions with different priorities and due dates. Manual follow-ups may be inconsistent, and owners may not have a clear view of all their outstanding tasks.

This project addresses these challenges by automating the identification of overdue tasks, grouping them by owner email, and preparing email notifications containing the relevant task details.

## Project Objectives

* Automatically retrieve task records from an Excel tracker stored in OneDrive.
* Identify tasks whose status is marked as `Overdue`.
* Group overdue tasks by owner email address.
* Generate a formatted HTML table containing each owner's overdue tasks.
* Send consolidated email notifications to the relevant owners.
* Reduce repetitive manual work and support timely task resolution.

## Tools and Technologies

| Tool                     | Purpose                                            |
| ------------------------ | -------------------------------------------------- |
| Microsoft Power Automate | Workflow orchestration and automation              |
| Microsoft Excel          | Task tracking and source data                      |
| OneDrive                 | Cloud storage for the Excel workbook               |
| Microsoft Outlook        | Delivery of email notifications                    |
| HTML                     | Formatting task details into readable email tables |

## Source Data

The workflow reads task information from an Excel table containing the following fields:

| Column       | Description                                       |
| ------------ | ------------------------------------------------- |
| Action ID    | Unique identifier for each task                   |
| Action Title | Description of the task or action required        |
| Owner        | Person responsible for the task                   |
| Owner Email  | Email address used to deliver notifications       |
| Department   | Department responsible for the action             |
| Priority     | Task priority level                               |
| Status       | Current task status, including `Overdue`          |
| Start Date   | Date the task commenced                           |
| Due Date     | Expected completion date                          |
| Days Overdue | Number of days the task has exceeded its due date |

The Excel data must be formatted as a table so that Power Automate can retrieve the records through the Excel Online connector.

## Workflow Logic

The automation follows these steps:

1. **Manual trigger:** Starts the flow when required, allowing the workflow to be tested or run on demand.
2. **Retrieve task records:** The Excel Online connector's `List rows present in a table` action retrieves records from the workbook stored in OneDrive.
3. **Filter overdue tasks:** A `Filter array` action retains records where `Status` equals `Overdue`.
4. **Prepare owner emails:** A `Compose` action supports the preparation of the owner email list for processing.
5. **Filter by owner:** A second `Filter array` action identifies the overdue tasks associated with the owner currently being processed.
6. **Generate an HTML table:** The `Create HTML table` action formats the relevant task records into a structured table for email delivery.
7. **Send notifications:** The Outlook `Send an email (V2)` action delivers the notification and task details to the relevant owner.

The intended outcome is one consolidated email per owner containing all overdue tasks assigned to that person, rather than separate emails for individual tasks.

## Example Notification

The email notification can include:

* A brief message informing the owner of their overdue tasks.
* A table listing each overdue action.
* The action ID and title.
* Priority and due date.
* Number of days overdue.
* A request to review and resolve outstanding actions.

This format gives recipients a practical summary of their outstanding responsibilities without requiring them to search through the entire tracker.

## Key Benefits

* **Reduced manual effort:** Minimises the need to identify overdue tasks and prepare follow-up emails manually.
* **Consolidated communication:** Groups multiple overdue tasks into a single notification per owner.
* **Improved accountability:** Makes outstanding actions and responsible owners more visible.
* **Better prioritisation:** Provides task priority, due dates, and overdue duration to support follow-up decisions.
* **Repeatable process:** Uses defined filtering and notification logic to apply consistent rules whenever the workflow runs.

## Testing and Validation

The workflow should be tested against representative task records to verify that:

* Only tasks with `Status = Overdue` are included.
* Each overdue task is assigned to the correct owner email.
* Owners with multiple overdue tasks receive one consolidated notification.
* The HTML table displays the correct task details.
* Tasks with missing owner email addresses are handled appropriately.
* Empty result sets do not generate unnecessary emails.

## Limitations and Future Improvements

Potential enhancements include:

* **Scheduled execution:** Replace or supplement the manual trigger with a recurrence trigger for automatic daily or weekly checks.
* **Duplicate notification prevention:** Track notification status or last-notified date to prevent repeated emails on subsequent runs.
* **Escalation rules:** Notify supervisors when tasks remain overdue beyond a defined threshold.
* **Priority-based escalation:** Apply different follow-up rules to high-priority tasks.
* **Notification audit trail:** Record notification timestamps and delivery outcomes for monitoring.
* **Improved reporting:** Build a Power BI dashboard to track overdue tasks, departmental performance, and overdue duration.

## Conclusion

Overdue Task Automation demonstrates how Microsoft Power Automate can integrate Excel, OneDrive, and Outlook to streamline operational follow-up. By filtering overdue actions and consolidating them into owner-specific email notifications, the workflow provides a practical foundation for improving task visibility, accountability, and follow-up efficiency.


**Note:** This project automates the notification process; it does not automatically resolve tasks or guarantee that recipients act on the notifications.
