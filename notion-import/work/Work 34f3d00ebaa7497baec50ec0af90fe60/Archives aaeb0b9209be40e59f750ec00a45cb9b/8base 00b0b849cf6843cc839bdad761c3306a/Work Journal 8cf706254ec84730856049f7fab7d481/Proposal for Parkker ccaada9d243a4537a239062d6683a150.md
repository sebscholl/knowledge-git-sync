# Proposal for Parkker

Created: February 5, 2020 12:31 PM

The scope of this project contains the deliverables required for a successful product launch. That includes:

Roles:

- *App User* - A user of the mobile application.
    - Can add and manage their own vehicles.
    - Can create and manage their own profile and settings.
    - Can add and manage their own payment methods.
    - Can create a new parking sessions for their vehicles.
    - Can review and pay their own tickets.
- *Lot Owner* - An owner of one or more parking lots.
    - Can create and manage a Parkker account.
    - Can add and manage their own parking lots.
    - Can add and manage *Lot Managers* and *Lot Enforcers* to one or more of their parking lots.
    - Can create and manage *Lot Manager* and *Lot Enforcer* permissions for different parking lots (e.g. an enforcer can tow vehicles or a manager can updating pricing.)
    - Can create and manage lot permit types (hourly, daily, monthly) and promotions.
    - Can write and revoke issued tickets.
    - Can add and manage bank and account billing information.
    - Can review performance across all parking lots belonging to their account.
- *Lot Manager* - A manager of one or more parking lot's.
    - Can have **all same permissions as *Lot Owner*, as granted by the *Lot Owner.***
    - Can review performance across all parking lots they manage.
    - **Cannot** add and manage bank and account billing information.
- *Lot Enforcer* - A user of the web and mobile application who assigns tickets in assigned lots and towing orders.
    - Can write and manage their own tickets issued.
    - Can review commissions earned/owed from their own tickets issued.
    - Can issue towing and boot warrants, as specified by lot owner/manager.
    - Can search parking lots by *Lot Number* when issuing tickets.
    - Can look up registered vehicles by license plate when validating parking sessions.
    - Can add and manage bank and 1099 employment details.
- *Administrator* - A Parkker employee.
    - Can review and manage all Parkker accounts (full admin access to customer accounts)
    - **Cannot** review or update customer bank account or routing numbers.
    - Can review admin dashboard and KPI metrics.
    - Can freeze/delete customer accounts.
    - Can run monthly distribution payouts to owed parties (*Lot Enforcers* and *Lot Owners*)

***NOTE: A user should be able to have one or more roles, allowing them to use the platform fully through a single user account.***

- Parkker Mobile Parking app with the listed flows enabled:
    1. User login / sign-up / logout / forgot password flows.
    2. User on-boarding flow: 
        1. (*If SMS authentication is used*) A new App User should be prompted to enter a verification code sent to them via SMS.
        2. A new App User should be guided through the steps of building out their profile and adding their primary vehicle and payment information.
    3. New parking session flow:
        1. An App User should be able to enter a parking lot number, or select from a list of recently visited lots, when starting a new parking session.
        2. After specifying the lot, an App User should be able to specify:
            1. The vehicle they are parking
            2. A space number
            3. A unit number (when applicable) 
            4. An available permit type
            5. A payment method
            6. Whether to auto-renew (when applicable)
            7. A promo code (when available) 
        3. After creating a new session, a user should be displayed a *success* message in a session details page.
    4. Account, settings, and billing flows:
        1. An App User should be able to add one or more payment methods (CC, Debit, Bank) to their account, as well as specify a "primary payment method" to be used by default.  
        2. An App User should be able to update their User Profile, Language Settings, Currency Settings, Notification Settings (SMS, Email, or Push on parking expiring/expired, ticket issued, or payment failed).
            1. *Note: All these screens will be standard forms. The exact details collected and stored can be defined flexibly without changing project scope.*
        3. An App User should be able to delete their account if **all outstanding tickets have been paid.**
    5. Vehicle management flows:
        1. An App User should be able to add, update, and delete vehicles from their account, as well as specify a "primary vehicle" to be selected by default while parking.
        2. For every vehicle, an App User should be able to specify the License Plate Number, State, and an optional nickname (to be displayed in place of the license plate number).
    6. App history flows:
        1. An App User should be able to review their parking history on both an account level and per vehicle level.
        2. An App User should be able to review their ticket history on both an account level and per vehicle level, as well as clearly see tickets unpaid.
        3. An App User, when reviewing Ticket History or Parking History, should be able to see a total spent during a specified time period (default to past 30-days or since beginning of month)
    7. Ticket payment an penalty flows:
        1. An App User should **not** be allowed to create new parking sessions when there are un-paid tickets on their account.
        2. If there are un-paid tickets on an App Users account, the system should prompt them to pay their tickets while trying to start a new parking session.
        3. An App User should be notified when their vehicle has been towed or booted, along with any instructions required to recover the vehicle.
    8. Enforcer search flows:
        1. A Lot Enforcer should be able to search vehicles by plate in the lots that they are assigned to enforce.
        2. If the vehicle has **no** permit to park, the Lot Enforcer should be prompted to issue a ticket.
    9. Ticket issuance flows:
        1. When issuing a ticket, a Lot Enforcer should be able to:
            1. Add one or more violations.
            2. Upload one or more photos of the vehicle.
            3. Confirm the license plate number.
            4. Add free form text notes that are displayed only to the Lot Manager.
            5. Submit the ticket.
        2. When a ticket has been approved by the Lot Manager, the Lot Enforcer should receive a notification that their ticket was approved.
    10. Enforcer profile flows:
        1. At any time, an Lot Enforcer should be able to review a list of all tickets issued and review issued tickets by state (pending, approved, rejected, and paid) for a specified date range (default to since last payout).
        2. A Lot Enforcer should be able to see their *Revenue Share %*, as well as a high level earning summary.
        3. A should be able to add and manage bank and 1099 employment details in their account.

- Parkker Web app with the listed flows enabled:
    
    *Note: Since a Lot Owner and Lot Manager can have the same permissions, please consider the following flows as ones available to **Lot Admins**, as restricted by the Lot Owners configuration settings.*
    
    1. User login / sign-up / logout / forgot password flows.
    2. User on-boarding flow: 
        1. A new Lot Owner should be prompted to verify their email address before setting up their account.
        2. A new Lot Owner should be walked through the steps of setting up their first parking lot and space inventory upon signing up. 
        3. During the onboarding flow, a Lot Owner should be prompted to add Lot Managers and Lot Enforcers to their properties (optional).
        4. After setting up their first parking lot, the Lot Owner should be displayed an option to purchase all required signage that will be needed on the property.
    3. Managing account flow:
        1. A Lot Owner should be able to update billing and payment information on their account. 
        2. A Lot Owner should be notified clearly that all payments will be with-held by Parkker until a valid bank account is linked to their account.
        3. A Lot Owner should be able to enter and update all their own account information and notification settings.
    4. Managing employees flow:
        1. A Lot Owner should be able to invite employees by email address to set up Parkker accounts.
        2. A Lot Owner should be able to specify the level of permission that a Lot Enforcer and Lot Manager with have, such as:
            1. Lot Manager can update permit pricing.
            2. Lot Manager can add new parking lots.
            3. Lot Enforcer can order vehicle to be towed/booted.
    5. Managing parking lots flow:
        1. A Lot Owner should be able to add parking lots to their account by specifying all required information, such as:
            1. Name
            2. Address
            3. Notices
            4. Space numbers
            5. Unit numbers
            6. Promotion Codes
            7. Hourly, Daily, and Monthly permit settings
            8. Tax Rate
        2. A Lot Owner should be able to delete a parking lot.
        3. A Lot Admin should be able to update all settings for a parking lot without the system changing issued permits until the subsequent billing cycle.
        4. A Lot Admin should be able to blacklist plates from parking their parking lots.
        5. A Lot Admin should be able to add and remove Lot Enforcers from their parking lots by email address.
        6. A Lot Admin should be able to update and share promo codes for a specific parking lot. 
            1. A promo code should be able to be assign directly to an App User profile, restricted to a specific number of uses, assigned an expiration date, or public.
            2. A promo code can be configured to grant a percentage discount, static amount discount, or free time-period. 
        7. A Lot Admin should be able to add and manage Violation Types to be assigned to tickets.
    6. Reviewing session flow:
        1. A Lot Admin should be able to review all sessions in one or more of their lots. 
        2. A Lot Admin should be able to filter sessions using a number of standard filters, such as:
            1. Lot ID/Name
            2. Date Range
            3. Charge Amount
        3. A Lot Admin should be able to export/print any list of Session Data to an Excel, PDF, or CSV document.
        4. A Lot Admin should be able to view high level charts and aggregated metrics that reflect all or filtered parking session data.
    7. Managing tickets flow:
        1. A Lot Admin should be able to review all tickets in one or more of their lots. 
        2. A Lot Admin should be able to filter tickets using a number of standard filters, such as:
            1. Lot ID/Name
            2. Date Range
            3. Fee Amount
            4. Enforcer Issue By
            5. Plate Number
            6. Ticket Status
        3. A Lot Admin should be able to reject or approve tickets issued by a Lot Enforcer, with the option of specifying an penalty type:
            1. When a Lot Enforcer selects an enforcement option, the system should:
                1. (When issuing a ticket) - Notify the Lot Manager and App User
                2. (When booting the vehicle) - Notify the Lot Manager for approval
                3. (When towing the vehicle) - Notify the Lot Manager for approval
        4. A Lot Admin should be able to view high level metrics showing ticket revenue realized, owed, and rejected during any given time period.
    8. Help flow:
        1. A Lot Admin should be able to easily get help and find educational resources on how the use the Parkker app in an information page.
    9. Administrator flow:
        1. An Administrator should be able to review all customer accounts, as well as manage the non-sensitive information and settings saved to that account, such as:
            1. An Administrator can delete a user's parking lot.
            2. An Administrator cannot review/update/change a user's bank information.
        2. An Administrator should be able to review a high level overview of revenue received by customers (customer revenue) and from customers (Parkker revenue) from all or filtered account data.
        3. An Administrator should be able to add, edit, and delete Help Page articles in the application.
        4. An Administrator should be able to add **other administrators**.
        5. An Administrator should be able to specify the amount ($) per parking space that a customer account will be billed. 
        6. An Administrator should be able to view any customer's Parkker account as that customer, with necessary restrictions on data access.
        7. An Administrator should be able to delete a customers account with all associated data.
- 3rd Party Integrations
    1. Payments / Payouts flows (options include PayPal API, Braintree API, [Authorize.net](http://authorize.net) API):
        1. An App User should be able to link up a payment provider or enter credit card information so that Parkker can charge the App User for permits and tickets.
        2. A Lot Owner should be able to link up a payment provider or enter credit card information so that Parkker can charge them for monthly subscription fees.
        3. A Lot Owner and Lot Enforcer should be able to link up a bank account so that they can receive payout distributions from Parkker.
    2. Email / SMS flows (options include SendGrid + SNS, Twillio, and others):
        1. Parkker should be able to send manual or automated messages to users as notifications in app, as well as via email and SMS.