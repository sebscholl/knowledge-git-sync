# Salesforce App Idea

Story:

Not-a-Loan is an equipment financing company that deals with 10,000's of small business owners across the US. Their sales-reps are totally overwhelmed with processing loan applications, which have been the main time-suck from them focusing on new and existing growth opportunities.

This bottleneck has led to many missed opportunities and angry customers. As a result, the CEO, David, has decided that they need to move away from manually processing applications and invest the time and money into an automated workflow approach.

After some research, David came across 8base's Bolt product and became convinced that it would be the most cost-effective and pain-free way to access their customer data - which all lives in Salesforce.com. David does not employ any professional Salesforce.com developers but he does employ JavaScript developers.

David's main concern is timeliness on this project. The company is unable to grow if this isn't figured out and some key players on his sales team have expressed frustration in with the company.

David decides he will dedicate one front-end JavaScript developer, who is also a fan of GraphQL and has been tinkering with it, to work with 8base Bolt to create a self-service equipment financing application app.

Overview:

An app will be created using React and GraphQL to enables a web front-end for businesses to apply for equipment financing. Customers will authenticate into the React app and will be linked to their customer profile in SalesForce.com.

An automated workflow for sales-reps to create an opportunity in Salesforce and then have all the "busy-work" handled (sending of documents and populating of important fields with progress indicators for application tasks completed / uncompleted). Additionally, any customer applying for financing should have a login dashboard to see the state of their applications.

Spec:

Stipulations:

1. For privacy reasons NO customer information currently stored in Salesforce can be replicated in 8base (with the exception of a userId).
2. In a loan document data, if a customer field is available in Salesforce, it should be automatically populated in the document.

Flow

1. When a customer is tagged "application processing" in Salesforce, a new "ApplicationProcess" is created in 8base
2. The "ApplicationProcess" has many predefined "Tasks", each of which has a type - Sign, Collect, Review - and an assignee - Agent or Customer.
3. Each task is sequentially ordered and completed - meaning one is supposed to be done after the other - and once done gets marked as "Completed"
4. Tasks can have a File or Image attachment and collect input data

Customer

1. When a customer's record is tagged in "application processing" in Salesforce, 8base sends them an email saying "Track your application status by creating an account at Not-A-Loan.com"
2. If when the customer logs in, they will see all their applications with statuses indicating Processing, Denied, Approved
3. When clicking on an application, they have displayed any Tasks that are pending their action, as well as tasks pending the agent's action.
4. Whenever a Task is queued that demands either parties attention, they are notified via email.
5. All documents attached to tasks populate customer information in the document with Salesforce data and collects additional data via in-app forms
6. A customer can see what information the Not-a-Loan has about them and create a "ChangeRequest" for data that should be updated or changed

Sales Agent

1. When an agent updates tags a customer "application processing" in Salesforce, all next steps (Tasks) are populated for them in the Not-a-Loan app with the relevant documents
2. Whenever customers records are tagged "application processing", "application denied", "application approved" in Salesforce, they're Not-a-Loan dashboard updates accordingly.
3. Whenever a data field is updated in Salesforce (like, LastName), the Tasks that make use of that data reset their status to re-prompt the agent and user of needed updates/actions.
4. When a Customer is deleted in Salesforce, the ApplicationProcess is removed from Not-a-loan.com
5. When a ChangeRequest is made, it's received by the salesperson who can deny it or have it automatically marked "Complete" by updating the entry in Salesforce.

Manager

1. As a manager, David will be able to see how many applications each agent is processing.
2. Drilling in, he can view approval / denied rates, and "time-per-application" on an organizational/single agent level.
3. Time is tracked on each application for how long in aggregate it took each party (customer and agent) to complete all their tasks
4. Once all tasks as completed, the ApplicationProcess is sent to David for the final approval/denial, with all documents and attachments included