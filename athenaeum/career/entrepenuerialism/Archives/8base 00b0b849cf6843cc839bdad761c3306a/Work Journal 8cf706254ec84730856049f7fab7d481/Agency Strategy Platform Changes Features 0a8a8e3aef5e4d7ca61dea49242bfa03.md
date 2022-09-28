# Agency Strategy Platform Changes/Features

Created: July 1, 2020 12:22 PM

The following feature updates would enhance our ability to roll out a sales strategy targeted at agency customers.

### Agency Plan

The agency plan is different from our historical plans in that the Developers limit (Collaborators) exists at the License level, **not** the workspace level. These Agency licenses start at $250/mo for 5 developers, and then increase at $50/mo/developer; with other scaling factors being increased/decreased not on usage or workspace factors (i.e, support and training).

Additionally, the Agency License pricing should be able to have pricing set on a per customer basis, since there will likely be negotiations on support, user seats, and other factors that effect pricing on a per customer basis.

This is a fundamentally new concept in the 8base system, as the billing plan is in relation to a "Group" and not a workspace.

### Organizations

An Organization enables its Owners and Admins to manage developer seats across organization owned Workspaces. Organizations can be created from the Developer Home Screen.

### Agency Workspaces

An Agency License will give access to 3 types of 8base Workspace Plans.

- *Agency_Sandbox_Workspace:* Every Agency customer gets 1 sandbox workspace included with their license and they are able to purchase more at $25/mo/workspace.
    - The goal of *Agency_Sandbox_Workspace's* is to allow their developers a playground environment for testing ideas and learning.
    - This plan has the same usage limits as our current Developer plan, though with **all features enabled**.
    - Any developer on the Agency license can get invited to an *Agency_Sandbox_Workspace.*
- *Agency_MVP_Workspace*: This workspace is identical to our current $49/mo Developer+ plan, though having **Service Premiums** enabled.
    - The goal of *Agency_MVP_Workspace's* is to provide agencies with a low-cost workspace in which they intend to develop fast and not worry about CI/CD.
    - This plan will be priced at **$75/mo/workspace**.
    - Any developer on the Agency license can get invited to an *Agency_MVP_Workspace.*
- *Agency_Professional_Workspace*: This workspace is identical to out current $149/mo Professional plan though having **CI/CD and Service Premiums** enabled.
    - The goal of *Agency_Professional_Workspace's* is to provide agencies with an end-to-end backend resource, handling all dev, stage, and production environments, while providing high enough usage limits for production and growth stage apps.
    - This plan will be priced at **$175/mo/workspace**.
    - Any developer on the Agency license can get invited to an *Agency_Professional_Workspace*
    

### **Service Premiums on Workspace Subscriptions**

Service Premiums are a new feature that will only be enabled to *Agency_MVP_Workspace* and *Agency_Professional_Workspace* plans. They allow the workspace owner (an Agency License Manager), to **set a premium that get's charged on-top-of the workspace's subscription amount** to the card on file. It also let's them set a custom description that will get used for the statement transaction line-item.

- The goal of **Service Premiums** is to help Agencies build a compelling business case for using 8base by facilitating their own re-occurring revenue through client projects backends.
- Using the Stripe Transfer API, we'll be able to transfer an Agencies owed Service Premiums to a connected account before the funds become available in 8base's own Stripe account ([https://stripe.com/docs/api/transfers/create](https://stripe.com/docs/api/transfers/create)). This is important to our own accounting.
- An Agency's bank details or Stripe account details get collected at the License level, as all agency payouts always go to a single account, whereas workspaces subscriptions go can run on different cards.
- **Service Premiums** allow agencies to enter their client's card for the 8base Subscription while still controlling the invoice description and their services revenue. For example, an Agency with 10 clients all on *Agency_MVP_Workspace's* charging a $100 Service Premium on every workspace will receive $1,000/mo from 8base in payouts.

### Agency Dashboard

Whether it is an Agency or Company, the concept of a "Group" that has associated developer accounts and own's project workspaces is a key component to rolling out this initiative. All developer account's will still be owned by developers themselves, meaning that a developer can get invited to join an Agency's Group, create an account, collaborate on the agency's projects, but still create their own Free Tier or Developer Plan workspaces.

Only an Agency's Group admin is able to create new workspaces within the Group on the Agency License, set Service Premiums, set Billing info, invite developers to the Group, and manage a developer's roles and permissions within the Group and Group owned workspaces.

### Agency Earnings Dashboard

To further encourage the understanding and acknowledgement of 8base being an business asset as opposed to an expense, a simple chart dashboard that shows the last month, next month, and year end expected revenue for **service premiums - license cost ****should get added to the license manager's home screen. This is intended to encourage them in using the product, as every-time they add a new client project with a service premium on 8base, their expect future revenue will rise.

In terms of budget, our pricing at 8base Labs is bespoke. We've agreed to take on projects for as little as $75,000, as much as $2,000,000, and everywhere in-between. The 2-primary driving factors being project complexity and timeline. In order to determine where your own project falls within that range, we'll have to have a subsequent scoping call with one of our technical resources.