# Project Specification for Virtual Vision

This spec details two applications that when used together can administer a Visual Field Test, akin to that of the Humphrey Machine.

## Application One: VF Web Portal

A Web-based Portal in which *Clinicians* can login to administer Visual Field Test, review patient test history, review patient test performance, and allows *Admins* to manage *Clinician* accounts, register devices, add offices, and perform all other actions permitted to *Clinicians*.

### Roles

- *Admin* - An app user who is responsible for creating and managing *Technician*'s accounts under a specific practice/hospital software license.
- *Technician* - An app user who is a medical professional that is capable of administering Visual Field Tests.

### Tables

The following tables describe a data model that defines the relationships between different information that is to be collected and stored in the application database. 

*R -* Denotes a required field.

*U -* Denotes a unique field.

*E ( a, b, n )* - Denotes an enum with possible values.

*D ( a ) -* Denotes a fields default value.

**Licenses** - A table in which *Licenses* get stored, representing the top level tenant record.

**Table Fields**

- Customer_Reference_Name - *String -* The Customer's name (business, hospital, or individual) [ *R* ]
- Customer_License_Id - *String* - The Customer's license number.  [ *R U* ]
- Number_User_Seats - *Number -* How many user's will be permitted on the license. [ *D ( 100 )* ]

**Table Relationships**

- Users - *has_many*
- Patients *- has_many*
- Devices *- has_many*
- Patterns *- has_many*
- Strategies *- has_many*
- Offices - *has_many*

**Offices** - A table in which office locations get stored.

**Table Fields**

- Name - *String* - The Office's name.
- Address_1 - *String* - The Office's address 1.
- Address_2 - *String* - The Office's address 2.
- City - *String* - The Office's city.
- State - *String* - The Office's state.
- Zip- *String* - The Office's city.
- Country - *String* - The Office's country.

**Table Relationships**

- Users - *has_many*
- Devices *- has_many*
- License *- has_one* [ *R* ]

**Users** - A table in which *User* records get stored.

**Table Fields**

- **Email** - *String -* The User's email address [ *R U* ]

**Table Relationships**

- *License* - *has_one*

**Patients** - A table in which *Patient* records get stored.

**Table Fields**

- First_Name - *String -* The Patient's first name. [ *R* ]
- Middle_Name - *String* - The Patient's middle name.
- Last_Name - *String* - The Patient's last name. [ *R* ]
- Birthday - *Date -* The Patient's birthday. [ *R* ]
- Gender - *String -* The Patient's gender. [ *R E ( male, female, other )* ]
- MRN - String - The Patient's medical record number.

**Table Relationships**

- Examinations - *has_many*
- PatientEyeSettings - *has_many*
- PatientMedialHistory - *has_one* [ *R* ]

**PatientEyeSettings** - A table for storing known conditions about a users eyes.

**Table Fields**

- Eye - *String -* Indicates which eye. [ *R E ( Left Right )* ]
- Sphere - *Number -* Known eye condition value.
- Cylinder - *Number -* Known eye condition value.
- Axis - *Number -* Known eye condition value.

**Table Relationships**

- Patient - *has_one* [ *R* ]

**PatientMedicalHistories** - A table in which patient medical history data gets stored.

**Table Fields**

- Diabetes - *Boolean* - Whether or not the patient has diabetes [ *D ( undefined )* ]
- Hypertension - *Boolean* - Whether or not the patient has hypertension [ *D ( undefined )* ]
- Glaucoma - *Boolean* - Whether or not the patient has glaucoma [ *D ( undefined )* ]
- Diabetic_Retinopathy - *Boolean* - Whether or not the patient has diabetic retinopathy [ *D ( undefined )* ]
- Macular_Degeneration - *Boolean* - Whether or not the patient has macular degeneration [ *D ( undefined )* ]
- Visual_Field_Issues - *String* - Extra known information about issues with the Patient's visual field.
- Drops - *String* - Extra known information about drops the Patient uses
- IOP - *String* - Unknown.
- IOP_TMAX - *String* - Unknown.

**Table Relationships**

- Patient - *has_one* [ *R* ]

**Patterns** - A table in which different Visual Field Test patterns get stored.

**Table Fields**

- Name - *String* - The Visual Field Test pattern. [ *R U* ]
- Public - *Boolean -* Whether or not the pattern is accessible to all Licenses. [ *D ( true )* ]

**Table Relationships**

- Examinations - *has_many*
- Licenses - *has_many*

**Strategies** - A table in which different Visual Field Test strategies get stored.

**Table Fields**

- Name - *String* - The Visual Field Test strategy. [ *R U* ]
- Public - *Boolean -* Whether or not the strategy is accessible to all Licenses. [ *D ( true )* ]

**Table Relationships**

- Examinations - *has_many*
- Licenses - *has_many*

**Devices** - A table in which Visual Field Testing devices (HMD Headsets) are tracked.

**Table Fields**

- Name - *String* - The devices name. [ *R* ]
- Device_Code - *String -* The devices hardware ID [ *R U* ]

**Table Relationships**

- Examinations - *has_many*
- License - *has_one* [ *R* ]
- Office - *has_one*

**DevicesRegistrationToken** - A table in which registration tokens get stored for Visual Field Testing devices (HMD Headsets).

**Table Fields**

- Code - *String* - The registration code [ *R U* ]
- ExpirationDate - DateTime *-* The day and time at which the token expires [ *R D ( created_at + 5:00 )* ]

**Table Relationships**

- License - *has_one* [ *R* ]
- Device - *has_one*

**Examinations** - A table in which *Examinations* get stored.

**Table Fields**

- Status - *String -* The status of the examination. [ *R D( pending ) E ( Queued "In Progress" Completed )* ]
- Stimulus_Size - *String* - The size of the stimulus to be used during the Visual Field Test. [ *R E ( III )* ]
- Eye - *String* - The eye(s) that will be tested during the Visual Field Test.  [ *R E ( Left Right Both )* ]
- Language - *String -* The language in which the Visual Field Test will be administered. [ *R E ( English Spanish Russian Polish Chinese Hindi )*  ]
- Fixation_Target - *String -* The point in which the *Patient* should focus during the Visual Field Test. [ *R E ( "Central Point" )* ]
- Show_Instructions - *Boolean -* Whether or not instructions should appear during the Visual Field Test. [ *D ( true )* ]
- Foveal_Threshold - *Boolean -* Whether or not a *Foveal Threshold* will be used during the Visual Field Test. [ *D ( false )* ]
- Exam_Date - *DateTime -* The date and time during which the Visual Field Test was administered.

**Table Relationships**

- Patient - *has_one* [ *R* ]
- Pattern - *has_one* [ *R* ]
- Strategy - *has_one* [ *R* ]
- Device - *has_one* [ *R* ]
- Office - has_one
- ExaminationReport - has_one

**ExaminationReports** - A table for storing Examination reports for Visual Fields Tests.

**Table Fields**

- Status - *String -* The status of the ExaminationReport. [ *R E ( Processing Processed ) D ( Processing )* ]
- Duration - *Number -* The total number of seconds in which the Visual Field test was completed. [ *R* ]
- Report - *File (PDF) -* The final PDF Visual Field Test results report generated. [ *R* ]
- Raw_Results - *JSON -* A *JSON* object storing all raw results (RealTimeTestResults) collected during the during the Visual Field Test. [ *D ( {} )* ]
- Imaging_Device_Brightness - *String -* A value denoting the devices screen brightness.
- Visual_Points_Count - *Number -* The number of visual points used during the Visual Field Test.

**Table Relationships**

- Examination - *has_one* [ *R* ]
- Patient - *has_one* [ *R* ]

**RealTimeExamResults -** A table for storing data from Visual Field Tests in real-time.

**Table Fields**

- Type - *String -* Whether the result is a false positive or a false negative. [ *R E ( t_pos f_neg f_pos  )* ]
- X_pos - *Number -* A number value indication the X coordinate position of the light shown.
- Y_pos - *Number -* A number value indication the Y coordinate position of the light shown.
- Z_pos - *Number -* A number value indication the Z coordinate position of the light shown.
- Decibels - *Number* - A number value indication of the brightness of the light shown.
- Duration - *Number -* A number indicating for how many milliseconds the light was shown.

**Table Relationships**

- Examination - *has_one* [ *R* ]

### Role Based Flows

The following flows detail capabilities that should be enabled to users on a per role basis. Each workflow will manifest into an application screen, form, or other application component in order to benefit its intended user.

**All -** an app user should be able to...

- login and logout.
- reset their password if forgotten by receiving a forgotten password email.

**Admin -** an Admin should be able to...

- create, manage, and delete *Technician* app users under their respective license.
- create, manage, and delete office locations and devices under their respective license, as well as change settings around which Visual Field Test patterns and strategies are available to their *Technicians.*
- delete data belonging to patients and examination reports from under their respective license.
- perform **all** permission that are made available to *Technicians.*

**Technicians -** A Technician should be able to...

- list all devices belonging to their respective license, filtered by office if desired.
- initiate a new Visual Field Test examination.
- create new patients, or list past patients, when initiating a new Visual Field Test examination.
- configure a Visual Field Test examination, as well as edit/update information in regards to the patient's record and medical history.
- review Visual Field Test examination results in real time while the patient is performing a Visual Field Test examination.
- cancel or restart a Visual Field Test in the event that a technical or physical error occurred during testing.
- review, email, and print a patient's Examination Report once it's been processed.
- access a page containing relevant help materials and information regarding how to administer tests and perform basic setup of devices.

## Application Two: VF VR Simulator

A Virtual Reality App in which *Patients* can undergo a Visual Field Test when administered by a *Technician*.

### Roles

- *Patient* - An app user who is responsible for creating and managing *Technician*'s accounts under a specific practice/hospital software license.

### Role Based Flows

The following flows details the experience that should be enabled to Patients in the application. The flow will manifest into a virtual reality experience in order to benefit its intended user.

**Patient -** A Patient should be able to...

- Receive verbal and visual instructions regarding how to adjust the device and perform the Visual Field Test, in the language of their choosing.
- Use an input controller to indicate when they are ready to begin the Visual Field Test.
- Use an input controller to indicate their positive responses to any perceived visual stimuli.
- Receive verbal and visual instructions at each stages of the examination, including when the examination is over and they can remove the device.

## Development Stages

Each of the following development stages details possible technologies that can be used and required functionality in order to produce both applications; visual field VR Simulator and Web Portal.

### Stage 1: VR Simulator

**Technologies**

- Unity - Game editing IDE that's widely used for VR development.
- C# - Programming language in which the VR app will get written.
- Oculus Go (Hardware) - The Virtual Reality HMD for which the Simulator will be built.

**Application Setup (1 - 2 Days)**

Set up will involve configuring development environments, continuous integration and continuous development pipelines, and setting up Unity Cloud builds. This effort is dedicated to setting up development processes that allow for code stability, integrity, and versioning.

**Device Registration Scene  (1 Day)**

On application load, the VR Simulator app will check for a stored token that indicates whether or not it is running on a registered device. If the token is not present, a Device Registration Scene will load. If the token is present, an Examination Loading Scene will load.

In this scene, the *Technician* is able enter a registration code that will be collected from the VF Web Portal. **Once the token is entered, it will be submitted to the Web Portal API for validation. If valid, the scene will receive a success response and store the token on the device for later retrieval. If not valid, the *Technician* will be prompted to re-enter a valid token.

Until a device is successfully registered, no other application scene will be accessible. **

**Examination Loading Scene (1 Day)**

On scene load, the VR Simulator will query the Web Portal API for any queued Examinations belonging to it. If none are found, it will automatically retry the query after 10-seconds. Meanwhile, clicking the controller input trigger will also retry the query at the user's request.

When a queued Examination belonging to the current device is returned by the Web Portal API, the application will load the Examination Scene and all of the Examination settings will be read and used to guide the application in properly administering the Visual Field Test per the *Techni*c*ians* instructions. 

**Examination Scene (15 - 30 Days)**

On scene load, the VR Simulator will prepare the scene with the Visual Field Test specified to be administered in the Examination. In this scene, the *Patient* is able the undergo a Visual Field Test. Every Visual Field Test must be initiated ("Queued") by a *Technician* within the Web Portal.

When the Examination is ready, instructions will begin explaining to the *Patient* how to take the Visual Field Test. Once the instructions have ended, the *Patient* will be instructed to pull the controller input trigger when they are ready to begin the Visual Field Test.

The application will administer a 24-2 Visual Field Test on both or either of the *Patients* eyes, starting with the right eye and moving to the left eye. During the Visual Field Test, requests will be sent in real-time to the Web Portal API on the following events.

1. True Positive Stimulus - The *Patient* responded to the stimulus light within the calibrated time window.
2. False Positive - The *Patient* responded to no stimulus light.
3. False Negative - The *Patient* failed to respond to the stimulus light within the calibrated time window.

Light stimuli will be calibrated to appear within the *Patient's* field of view (FOV) for 250-milliseconds and allow 500-milliseconds for the *Patient* to respond; both clocks starting in tandem, allowing the response timer to run and additional 250-milliseconds after a stimulus light has been turned off.  

The VR Simulator will adjust the brightness of light stimuli using a step function that adjusts for 3-decibels at each step. *Brightness* will allow for calibration, and take into consideration adjustments to the devices set screen brightness.

When the Simulator has finished administering the Visual Field Test, the *Patient* will be instructed to remove the HMD. All final data collected during the administer Visual Field Test will be submitted to the Web Portal API, and the app will return to the Examination Loading Scene.

**Notes**

The whole VR Simulator can be developed **without** the Web Portal API and integrated at a later date. This allows for developers to work on separate applications in tandem while the VR Simulator uses static Examination settings for testing purposes. 

The large time window assumed for the **Examination Scene** is a result of uncertainty around stimuli calibration and specifics of the test sequence algorithm. With help from resources familiar with the inner workings of the Humphrey Test, this risk can be quickly mitigated.

### Stage 2: Web Portal API (Backend)

**Technologies**

- 8base - Backend technology for building application APIs and data storage.
- AWS Lambda - Functions-as-a-Service for building integrations between 8base and 3rd party systems.

**Application Setup (0.5 Days)**

Set up will involve configuring development environments, and continuous integration and continuous development pipelines. This effort is dedicated to setting up development processes that allow for code stability, integrity, and versioning.

**Data Model + Application Roles (1 Day)**

This stage will consist of configuring all data tables and table relationships, ensuring the logical separating are data records between customer Licenses. Additionally, application roles will be configured so that they each application user's permissions will be enforced at the API level.

**Business Logic (7 Days)**

All business logic as it pertains to the applications flows must get developed and deployed as server side code. This will encompass the adding of Users, registration of devices, creation of new exams and so forth. Based on the technologies used, many basic database API operations will be available and usable without custom code. However, all "workflow" based logic must be developed.

**Medical System Integration (1 - 14 Days)**

Potential time spent building integrations with existing Medical Record Systems for sending Visual Field Test examination reports and potentially reading Patient data.

**Statistical Analysis and Reporting (15 - 30 Days)**

After an Visual Field Test is administered, all data collected must be processed into an examination report and saved as a PDF. 

**Notes**

Much of the API development will be immediately available based on the proposed technologies. This cuts significant time of the potential development cycle. 

The large time window assumed for the **Statistical Analysis and Reporting** is a result of uncertainty around how analysis is performed on data received by the Visual Field Test examination. With help from resources familiar with the capture, interpretation, and presentation of simulation data, this risk can be quickly mitigated.

### Stage 3: Web Portal (Frontend)

**Technologies**

- Vue.js - Frontend JavaScript framework for building web applications.
- Vuetify - Vue.js based UI component library.
- Daedal Pro Theme - Vuetify theme with prebuilt styling and layout.
- Auth0 - Authentication provider for handling user authenticating in web and mobile apps.

**Application Setup (0.5 Days)**

Set up will involve configuring development environments, and continuous integration and continuous development pipelines. This effort is dedicated to setting up development processes that allow for code stability, integrity, and versioning.

**Application Design (0.5 Days)**

Borrowing from the screens found on https://[virtualfield.io](http://virtualfield.io/), the design of the Web Portal application can be greatly expedited. Branding variables such as colors, fonts, borders, images, and the like can all be customized.

**Patient Views (1 Day)**

These screens will allow an app user to review patients existing patients under their respective license, list all examinations the patient has completed for either or both eyes, and manage/delete the patient's data.

**Device + Address + User Views (0.5 Days)**

These screens will allow an app user to add and remove devices, users, and addresses under their respective license, as well as relate the two. Some of these abilities will be discoverable within a *Settings* screen, while others will have the own top level navigation pages.

**Help Views (0.5 Days)**

These screens will display static information and video content helpful to the app user in terms of "How to's" on administering tests and managing their license.

**Examination Views (1 Day)**

These screens will walk an app user through selecting a patient and entering their medical information along with the examination settings. Also, included will be instructions on how to help a *Patient* begin an examination using the selected device.

**Real-time Examination Viewer (3 - 7 Days)**

This screen allows the technician to review *Patient* examination results in real-time, during which they can visualize the incoming information stream to determine both completeness of the examination, as well as whether their are any issues with the placement or performance of the device.

**Notes**

The Web Portal frontend is a very straight forward application. The only challenging part will be the Real-time examination viewer. That said, it is more of a concern around the visualization of data, and will be mitigated along with the research and preparation that will be required for **Statistical Analysis and Reporting** in the Web Portal API.

## Summary

### Development Timelines

**VR Simulator**

Team Size: 1

Add. team productivity boost: 0%

Estimated development days to application completion:

- Low: 18-days
- ***Expected: 26-days***
- High: 33-days

Notes: none

**Web Portal API (Backend)**

Team Size: 1

Add. team productivity boost: +1 developer on integrations and alaysis for ~40% productivity boost. 

Estimated development days to application completion:

- Low: 24.5-days
- ***Expected: 39-days***
- High: 52.5-days

None: The integrations are not required in the beginning and can be added incrementally. This potentially shaves 1-day of the low estimate and 14-off the high estimate)

**Web Portal (Front-end)**

Team Size: 1

Add. team productivity boost: +1 developer for ~50% productivity boost. 

Estimated development days to application completion:

- Low: 6-days
- ***Expected: 9-days***
- High: 11-days

None: An extra developer would double the speed of any front-end work.

### Scenario 1

A single developer responsible for solely handling all development of each application.

Team Size: 1

Estimated development days:

- Low: 48.5-days
- ***Expected: 74-days***
- High: 96.5-days

### Scenario 2

Two developers, each assigned either the VR Simulator or Web Portal, while collaborating on integrations and analysis as it pertains to the Web Portal API (Backend).

Team Size: 2

Estimated development days:

- Low: 42.5-days
- ***Expected: 47-days***
- High: 59.1-days

### Scenario 3

Three developers, each solely responsible for all development in respect to a single application.

Team Size: 3

Estimated development days:

- Low: 24.5-days
- ***Expected: 39-days***
- High: 52.5-days