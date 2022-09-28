# Valerie Call Declare

Created: May 5, 2020 3:01 PM

Marketing site is on Wordpress (with LMS plugin)

Need integration with Wordpress to

Take an onboarding quiz (3 or 4 quizes)

Pulls in data from LinkedIn

Poding = groups

They have a company like meetup.

They need to tackle how to get added to groups. (When can you meet? What industry are you interested in? What levels are you experience?)

They have data for successful podding.

Meeting time of day is priority = 10

Industry = 5

Weighted questions help determine which groups they should be added.

Accountability quiz - what are you looking to achieve? Decision tree conversation for labeling people.

User can take courses on wordpress

View and apply to pods

- Pod leaders manage pods (just allow people to enter or exit)
- Pods can be opened or closed - only can apply to open pods
- People in pods can see pods page, which has meetings schedules

Directory is where:

- Search and view people as part of the program
- Search by name and company (past and present)
- User profile (what industries are they interested in, pull Volunteer experience from LinkedIn)
- Connect with people  (profiles show personal contact info)

Accountability Tracker:

- Like a budgeting tool, set a goal and set a budget (set a course and set a topic, and whether you watch it)
- Track attendance

Self sponsor vs company sponsor

Most of the data is in Salesforce, Hivebright

History of videos watch on their system

- Introduce pricing at $150,000k for dev with $25,000 design fee.
- If she scoffs at pricing, free design work is first bargaining chip
- There are multiple rolls and interfaces that need to be designed and considered here, which will invariably lead to multiple interfaces being designed.
    - PodMember - See resources belonging to their pod(s).
    - PodOwner - Manage pods belonging to them.
    - AppUser - Access/Edit their own information.
    - AppAdmin - Declare employee with full access.
    - AccountManager - Declare employee that manages and creates memberships.
    - ContentManager - Declare employee with create & edit content and quizzes.
    - ContentAdmin - Declare employee that can publish content and quizzes.
- There are five topics of development focus:
    1. Onboarding & Discovery - management and client facing tools for creating the different onboarding quizzes and presenting them to new users to get completed.
    2. Podding - management and client tools for validating whether a user is eligible to join certain pods, have them added by pod leaders, and a show page for calendaring and meeting schedules.
    3. Directory - Logged in users can search for other users by which companies they belong to (past and present) as well as by name. User profiles display personal contact information so that they can get in touch off line. Some data is pulled from LinkedIn to account profile.
    4.  Accountability Tracker - Goals can be set towards ones desired personal growth (i.e., "I want to become a more confident manager"), actions will get defined for achieving that goal (i.e., "attend *N* pod meetings, take course *X* and *Y*, and read *Z* by *A* date"). Using different data sources or an honors system, such actions would get validated.
    5. Analytics - A central system where all events desired to be tracked get sent for the convenient analyzation of user behavior and general usage. \
- We think that the best effort to spearhead would be:
    1. Onboarding and Discovery
    2. Podding
    3. Directory
- Both the *Accountability Tracker* and *Analytics* will/should have more integration work with their existing systems, which we should stay away from for now. While working which them, we'd gain insights into what they've done and be able to better scope the rest of the project in the future.
- The only integration work required for *Onboarding & Discovery, Podding, and Directory* is SalesForce and LinkedIn which are highly predictable.