# Issue Reporting Form
An automated solution built with Microsoft Forms, Power Automate, and SharePoint to streamline issue reporting and tracking for the regional Automation & Analytics team. 
The flow captures issue details, identifies the issuer and their manager, logs the data in a SharePoint list, handles attachments, and sends notifications via email and Teams. 
A secondary flow confirms resolution and closure, ensuring visibility and accountability for ad hoc tasks.


## Overview
As the Automation and Analytics team continues to expand its portfolio of projects, the frequency of day-to-day issues has also increased. These issues are often ad hoc in nature and can be overlooked or deprioritized by managers due to their informal reporting—typically via email or Teams messages. This results in delays in resolution and consumes valuable time that could be spent on ongoing development work.

To address this, a structured issue tracking system was needed—something that didn’t exist previously. The solution was to create an automated issue reporting and tracking mechanism using Power Platform tools.

### Stakeholders
The entire regional team that utilizes automation tools and analytics dashboards.

---

## Objectives
- Provide a centralized and structured way to report issues.
- Ensure all reported issues are tracked and not missed due to informal communication.
- Enable managers and team members to monitor and manage ad hoc tasks effectively.
- Ensure that issues are properly closed with confirmation from the original issuer

---

## Tools & Technologies Used

- Microsoft Forms: Used to collect issue submissions from users.
- Power Automate (Flow 1): Automatically registers submitted issues into a SharePoint list and sends a confirmation email to the issuer.
- SharePoint List: Serves as the central repository for all reported issues, including status tracking.
- Power Automate (Flow 2): Sends a follow-up email to the issuer once the issue is marked as resolved, requesting confirmation to close the issue.

---

## Workflow Description

The solution consists of two Power Automate flows that work together to manage the lifecycle of issue reporting and resolution.

### Flow 1: Issue Submission & Registration

**Trigger:** When a new response is submitted in the Microsoft Form

**Steps**:
1. **Compose Logo**
   - Prepares a branded element for email notifications.

2. **Get Response Details**
   - Retrieves all form inputs such as issue description, category, urgency, and issuer’s email.

3. **Search User**
   - Looks up the issuer in the organization directory using their email address.

4. **Get User UPN & Name**
   - Extracts the User Principal Name and display name for personalization and tracking.

5. **Get Manager Email**
   - Fetches the issuer’s manager email to include as CC in notifications.

6. **Create Item in SharePoint List**
   - Logs the issue with metadata:
     - Issue details
     - Issuer name and email
     - Manager email
     - Status = “Open”
     - Submission timestamp

7. **Condition: Attachment Handling**
   - Checks if the user uploaded a screenshot or file:
     - **If Yes:** Parse JSON attachment
