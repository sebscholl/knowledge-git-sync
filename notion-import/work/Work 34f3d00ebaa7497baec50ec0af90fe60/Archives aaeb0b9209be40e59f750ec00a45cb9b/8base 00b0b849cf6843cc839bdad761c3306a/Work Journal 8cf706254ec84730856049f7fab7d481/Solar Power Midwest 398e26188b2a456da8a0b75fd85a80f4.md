# Solar Power Midwest

Created: July 8, 2020 4:11 PM

## **Overview**

**Solar Power Midwest** (“Client”) ****is launching a new venture and software product to provide the solar power industry with a comprehensive CRM and Project Lifecycle Management System.

The company and its founder, **Jim Liacone**, bring extensive experience in the national solar industry, with an emphasis on sales and installations completed in and near Illinois. Jim has grown frustrated with the lack of adequate software solutions serving his industry and has identified an opportunity to commercialize his **vision as a SaaS solution provider.

Aside from bringing cutting edge technology to his own firm, Jim believes his solution has commercial viability as a micro-SaaS product serving other service providers across the global solar industry.

This document outlines **8base's** understanding of the **product scope** and proposed approach to building it in partnership with **Solar Power Midwest**.

Ultimately, the software solution will seek to streamline and simplify the customer relationship process, beginning with a lead, through project implementation, to operations and maintenance.

A staple platform to be developed is smart scheduling. This will allow users of the SaaS product to employ route optimization, which will mitigate the frivolous use of employee time and gas, as well as delays in converting accounts receivable.

## **Personas and Primary Persona-Related Functionality**

The following personas will be accommodated in this project:

- ***CustomerFieldWorker*** - A user under a customer license who works in the field on Solar Projects.
    - Can see their assigned jobs and tasks.
    - Can manage status' and creates notes on assigned projects and tasks.
    - Can create and manage their own profile and settings.
    - Can read and update own calendar.
    - Can read teams calendar.
- ***CustomerSalesRep*** - A user under a customer license who works in a sales capacity.
    - Can create customer leads and accounts.
    - Can manage assigned and self-created leads and accounts.
    - Can create and send invoices to customer for available products.
    - Can cancel and manage invoices sent to customers.
- **CustomerMarketingRep** - A user under a customer license who works in a marketing capacity.
    - Can create and update lead capture forms
    - Can import and manage digital marketing assets
- ***CustomerManager*** - A user under a customer license who is responsible for managing all account resources and users.
    - Can create, manage, and delete users to customer license.
    - Can create, manage, and delete project templates under license.
    - Can create, manage, and delete project defaults under license.
    - Can assign projects and tasks to users under license.
    - Can import customer data via CSV from other CRMs.
    - Can fully manage all license records, unless configured otherwise by *CustomerAdmin*, under the license.
    - Can perform all capabilities of *CustomerMarketingRep, CustomerSalesRep,* and *CustomerFieldWorker.*
- ***CustomerAdmin*** - A user in a customer license who purchased the license and is responsible for billing details and full license management.
    - Can add, manage, and remove billing details for license.
    - Can assign and remove *CustomerManager* role to/from user.
    - Can set visibility of projects for *CustomerManager.*
    - Can delete own license.
    - Can perform all capabilities of *CustomerManager.*
- ***AccountManager*** - A Solar Power Midwest (SPM) employee responsible for customer success.
    - Can read and manage customer licenses.
    - Can update limits on licenses (user seats, CRM records, etc.)
    - Can freeze / unfreeze customer accounts based on payment statuses.
- ***AccountAdmin* -** A Solar Power Midwest administrator.
    - Has full system access with full permissions on all records.
    - Can perform all capabilities of *AccountManagers.*
    

## **Application Types**

A desktop browser-based web application will be developed to manage the administrative aspects of the solution for Solar Power Midwest. The application will be responsive, although all mobile screen-types are not within the scope of this project.

A Progressive Web App will be developed for the customer experience, with the design being responsively optimized for handheld tablets. This application will serve both an office worker and field worker, and can be added to to home screen of a tablet device for quick access by the customer.

Both applications will get developed using a modern Javascript front-end framework (ReactJS or VueJS) and compatible with all modern browsers.

### Key System Flows

**Admin App -** Administrative backend flows happen in the Solar Power Midwest Admin App.

1. Authentication Flows:
    1. A SPM employee should be able to login using their SPM business email.
    2. A SPM employee should be able to reset a forgotten password via email.
    3. A SPM employee should be able to manage their own account information.
2. Customer Account Management Flows:
    1. A SPM employee should be able to list and search all customer by name, region, account status, and internally assigned account manager.
    2. A SPM employee should be able to create a new customer account while setting a specific number of user seats, CRM record rows, and other resources on a per license basis.
    3. A SPM employee should be able to pull up a full details view of the customer, giving them insights into number of Customer users, usage metrics, payment/billing history, and other relevant information.
    4. A SPM employee should be able to update a customer's billing/payment information and confirm that the new information is valid.
    5. A SPM employee should be able to freeze a customer's account when the last payment status is overdue. 
    6. A *AccountAdmin* should be able to delete a customers account after confirming the customer's full name in an input.
    

**Customer App -** CRM and project lifecycle management flows happen in the Solar Power Midwest Customer App.

1. Authentication Flows:
    1. An unregistered user should be able to sign up and create their own license with their own account attributed the *CustomerAdmin* role.
    2. A Customer should be able to login using an email and password.
    3. A Customer should be able to reset a forgotten password via email.
    4. A Customer should be able to manage their own account information.
2. CRM Flows:
    1. A *CustomerSalesRep* should be able to list, search, add, manage, and mark-for-removal leads and customers in the CRM.
    2. A *CustomerSalesRep* should be able to track correspondence and notes with their Customers in the CRM.
    3. A *CustomerSalesRep* should be able to create and send a customer invoice from the CRM.
    4. A *CustomerSalesRep* should be notified via email when an invoice they created has been paid/rejected.
    5. A *CustomerSalesRep* should be able to access uploaded marketing assets to send to leads and existing customers.
    6. A *CustomerMarketingRep* should be able to create, manage, and delete lead capture forms.
    7. A *CustomerMarketingRep* should be able to upload and manage digital marketing assets.
    8. A *CustomerMarketingRep* should be able to send emails to filtered lists of leads and customers from the CRM.
    9. A *CustomerManager* should be able to assign leads and customers to *CustomerSalesReps.*
    10. A *CustomerManager* should be able to export customer data from the CRM to a CSV file.
    11. A *CustomerManager* should be able to create, manage, and remove products from the CRM, which include images, descriptions, default pricing, and other industry specific information.
3. Project Lifecycle Management Flows:
    1. A *CustomerFieldWorker* should be able to review the tasks and projects assigned to them.
    2. A *CustomerFieldWorker* should be able to visualize their tasks on a map based on their location.
    3. A *CustomerFieldWorker* should be able to filter their tasks in a project (map and list view) by due date, and other status indicators.
    4. A *CustomerFieldWorker* should be able to visualize all their projects in (map and list view) with indicators for whether tasks are pending.
    5. A *CustomerFieldWorker* should be able to update the status of a task.
    6. A *CustomerFieldWorker* should be able to leave notes on a task, or a project.
    7. A *CustomerFieldWorker* should be able to upload pictures, videos, and documents to a project or task.
    8. A *CustomerFieldWorker* should be able to visualize the full overview of a project.
    9. A *CustomerFieldWorker* should receive daily emails summarizing their upcoming tasks for completion.
    10. A *CustomerFieldWorker* should be able to review their calendar with task due dates set automatically.
    11. A *CustomerFieldWorker* should be able to add their own events to their calendars.
    12. A *CustomerManager* should be able to review all their employees calendars, and filter scheduled tasks by project, due date, and other relevant attributes.
    13. A *CustomerManager* should be able to create project templates, differentiated by product types or customer segment types (agricultural, residential, etc.)
    14. A *CustomerManager* should be able to create project defaults, where specific users will automatically be assigned specific tasks within a project if not defined otherwise.
    15. A *CustomerManager* should be able to re-assign projects and tasks to users on their license.
    16. A *CustomerManager* should be able to visualize a dashboard showing current projects, their completion progress, pending items, past due items, and other helpful information.
    17. A *CustomerManager* should receive daily/weekly emails summarizing project activity
    18. A *CustomerAdmin* should be able to set projects to being private or public within a license, and assign users visibility when a project is private.
4. License Management Flows:
    1. A *CustomerManager* should be able to add, manage, and remove users from their license while assigning them *CustomerFieldWorker, CustomerSalesRep,* or *CustomerMarketingRep* roles.
    2. A *CustomerAdmin* should be able to assign a license user the *CustomerManagerRole.*
    3. A *CustomerAdmin* should be able to add/remove billing and payment information from their license.
    4. A *CustomerAdmin* should be able to add user seats and purchase higher limits for their license without speaking to a Solar Power Midwest sales rep.