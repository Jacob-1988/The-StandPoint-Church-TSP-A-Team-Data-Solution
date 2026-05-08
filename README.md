## The StandPoint Church (TSP) A-Team Data Solution
### Statement of Problem
Over the years and particularly in recent times, TSP has been  faced repeated with repeated incidents of loosing first timers who comes to the church either to stay or just on a visit. This became a recurrent decimal that required utmost attention.
 A good tracking system that monitors members inflow and outflow had not been in place. Hence, it became a need.  

 This project addresses that problem by developing a system that warmly receives a first timer to the church, assigns the first timer to a team member by the FTA_ID, the team member puts up a call that sets the ball rolling for a constant follow up.
Additionally, it is worthy of note that this project was splitted into weeks to ensure accuracy of inputed dataset.

### Table of Contents:
#### 1. Project Overview 
1.1. Solution Architecture Flow

#### 2. WEEK 1: Setup & Form Creation
- 2.1. Environment Setup & Project Planning
- 2.2.  FTA Personal Data Form Creation
- 2.3.  A-Team Feedback Form Creation

#### 3. WEEK 2: Automation with Google Apps Script
- 3.1. FTA ID Generation Script
- 3.2.  Auto-Assignment Logic
- 3.3.  Email Notification System

#### 4. WEEK 3: Data Processing & Metrics Calculation
- 4.1.  Dashboard Metrics Sheet Setup

- 4.2.  Feedback Analysis
- 4.3.  Data Validation & Quality Checks

#### 5. WEEK 4: Looker Studio Dashboard Development
- 5.1.  Looker Studio Setup & Data Connection
- 5.2. Dashboard Layout & Header Section
 

### Project Overview:
#### Objective: 
Build an end-to-end data solution to track First-Time Attendees (FTAs) from
initial contact through follow-up, with automated assignment and real-time dashboard
monitoring.

#### Key Components:
1. FTA Personal Data Collection Form (Google Forms)
2. A-Team Feedback Form (Google Forms)
3. Automated FTA Assignment System (Google Apps Script)
4. Analytics Dashboard (Looker Studio)

#### Expected Outcome:
A fully functional system that captures FTA data, automatically
assigns them to A-Team members, tracks follow-up progress, and visualizes key
metrics for church leadership.

#### WEEK 1: Setup & Form Creation
####  Objectives:
#### 2.1. Environment Setup & Project Planning
#### Tasks:
#### 1. Set Up Master Data Sheet
- Created a Google Sheet named "A-Team Master Data."
- Created the following tabs:
- ■ FTA_Responses: Will auto-populate from FTA form
- ■ Feedback_Responses: Will auto-populate from feedback form
- ■ A-Team_Members: Manual list of A-Team members
- ■ Assignment_Log: Track FTA assignments
- ■ Dashboard_Metrics: Calculated metrics for Looker

#### 2. Populated A-Team Members Sheet
-  Columns: Member_ID, Full_Name, Email, Phone, Max_Capacity,
Current_Load, Status
-  Add all A-Team member details
- Set Max_Capacity (e.g., 5 FTAs per member)
- Initialize Current_Load as 0
- Set Status as "Active"

#### 3. Documented Requirements
- Reviewed all form fields
- Created a data dictionary documenting each field, its purpose, and
validation rules
- Map the end-to-end user journey

#### 2.2: FTA Personal Data Form Creation
#### Tasks:
#### 1. Created New Google Form
-  Name: "TSP First-Timer Information Form"
- Description: "Welcome to The Standpoint Church! We're excited to have
you. Please share a few details so we can serve you better."
#### 2. Added Form Fields (in order): Section 1: Personal Information
- Email address (Required, Email validation)
- Full Name (Required, Short answer)
- Phone number (Required, Short answer with format hint:
+234-XXX-XXX-XXXX)
- Gender (Required, Multiple choice: Male, Female)
- Home Address (Required, Paragraph text)
#### 3. Section 2: Service Experience
- How was your overall service experience? (Required, Linear scale 1-5: Poor
to Excellent)
- How will you rate your WORSHIP experience? (Required, Linear scale 1-5:
Poor to Excellent)
- How will you rate your WORD experience? (Required, Linear scale 1-5: Poor
to Excellent)
- Any general feedback for us? (Optional, Paragraph text)
#### 4. Section 3: Connection Information
- Who invited you to TSP? (Required, Dropdown):
- ■ A friend
- ■ A worker in the church
- ■ Church member
- ■ Colleague
- ■ Spouse
- ■ Self (Social Media)
- ■ Self (Billboard)
- ■ Home cell
- ■ Other
- Would you like to be a member of TSP? (Required, Multiple choice: Yes,
Not yet, Maybe later)
#### 5. Section 4: Consent & Next Steps
I consent that my data provided in this form can be used by The
Standpoint Church as deemed appropriate (Required, Checkbox)
#### 6. Linked to Response Sheet
-  Responses was linked to "A-Team Master Data" → "FTA_Responses" tab
- Note: Timestamp and FTA_ID was  added via script
#### 2.3: A-Team Feedback Form Creation
### Tasks:
#### 1. Created New Google Form
- Name: "TSP A-Team Follow-up Feedback Form"
- Description: "Tracked follow-up interactions with assigned First-Timers."
#### 2. Added Form Fields: Section 1: Identification
- FTA ID (Required, Short answer - will be auto-populated via URL
parameter)
- A-Team Member (Required, Dropdown - populated from A-Team_Members
sheet)
#### 3. Section 2: Follow-up Stage Selection
- FTA Call (Required, Multiple choice):
- ■ 1st call (Actual contact)
- ■ 2nd call (Put a face to the name)
- ■ 3rd call (Check-up call)
- ■ M&G Attended
#### 4. Add Conditional Sections: Section 3: 1st Call Details (Show if "1st call" selected)
- Called (Required, Dropdown):
- ■ Yes
- ■ Yes, but not reachable
- ■ Yes, but switched off
- ■ Yes, but didn't pick
- ■ Yes, sent TSP communique
- ■ Yes, sent a message

○ Feedback (Required, Dropdown):
- ■ Closed
- ■ Just visiting
- ■ Out of town
- ■ Prayer request
- ■ Transport needed
- ■ Would love to join
- ■ Hope to visit again
- ■ Other

○ M&G Confirmation Date_on_1st_call (Optional, Dropdown with available

○ General feedback_on_1st_call (Optional, Paragraph)
#### 5. Section 4: 2nd Call Details (Show if "2nd call" selected)
-  Choose the date you met your FTA (Required, Date picker)
- General feedback_on_2nd_call (Required, Paragraph)
#### 6. Section 5: 3rd Call Details (Show if "3rd call" selected)
- General feedback_on_3rd_call (Required, Paragraph)
#### 7. Section 6: M&G Attended (Show if "M&G Attended" selected)
- M&G Confirmation Date_on_M&G_confirmation_call (Required, Dropdown
with dates)
-  General feedback_on_M&G_confirmation_call (Required, Paragraph)
#### 8. Configure Conditional Logic
- Use "Go to section based on answer" for the FTA Call question
- Set up sections to show/hide based on selection
#### 9. Link to Response Sheet
- Link responses to "A-Team Master Data" → "Feedback_Responses" tab

#### WEEK 2: Automation with Google Apps Script
-Objectives:
- Generate unique FTA IDs automatically
- Build auto-assignment logic for distributing FTAs to A-Team members
- Create an email notification system
- Test automation workflows

#### 3.1: FTA ID Generation Script 
-Task:
#### 1. Opened Apps Script Editor 
- In the "A-Team Master Data" sheet, went to Extensions → Apps Script
- Created a new project named "TSP A-Team Automation."
#### 2. Created FTA ID Generator Function
#### 3. Created Form Submit Trigger
-  In the Apps Script editor, clicked on Triggers (clock icon)
- Added trigger:     
    ■ Function: onFormSubmit
    
    ■ Event source: From spreadsheet 
    
    ■ Event type: On form submit
    
    ■ Saved
#### 4. Tested the Script    
- Submited a test response through the FTA form
- Verified FTA_ID is generated in the format: FTA-20260112-001
####  3.2: Auto-Assignment Logic
#### Task:
#### 1. Created Assignment Function
#### 2. Created Main Form Submit Handler
#### 3. Set Up Assignment_Log Sheet Headers
- FTA_Name
- FTA_Email
- Assigned_Member_ID
- Assigned_Member_Name
- Assigned_Member_Email
- Status
- Notes
#### 3.3: Email Notification System
#### Tasks:
#### 1. Created Team Member Notification Email
#### 2. Created FTA Welcome Email
#### 3. Created Error Notification Function
#### 4. Testeed All Automation
- Submitted multiple test FTA forms
- Verified FTA_IDs were generated correctly
- Confirmed assignments were balanced across team members
- Checked that email notifications were sent
- Reviewed the Assignment_Log for accuracy

####  WEEK 3: Data Processing & Metrics Calculation
#### Objectives:
#### 4.1: Dashboard Metrics Sheet Setup
#### Tasks:
#### 1. Created Metric Calculation Formulas. In the "Dashboard_Metrics" tab, created the
following structure: Summary Metrics Section:
- Total FTAs (All-time)
- FTAs This Month
- FTAs This Week
- FTAs Today
- Average Overall Experience Rating
- Average Worship Rating
- Average Word Rating
- Membership Interest Rate (%)
- Follow-up Completion Rate (%)
#### 2. Add Formulas for Summary Metrics
#### 3. Created Follow-up Tracking Metrics. Created a new section for follow-up metrics.
#### Tasks: 
-  Created FTA Source Analysis Table. Created a new section starting at row somewhat 20.
- Created A-Team Performance Table. Created a new section starting at row somewhat 30.
- Created Monthly Trend Data. Created a new section starting at row somewhat 50.
####  4.2: Feedback Analysis
#### Tasks:
- Created 1st Call Outcome Analysis. Created a new section.
- Created Response Time Tracking. Added a new column in the Assignment_Log
sheet called "Response_Time_Hours." Created an Apps Script function to calculate
response time:

- Set Up Automated Metric Refresh: Created a time-based trigger to refresh metrics
daily:
    
     -  Function: calculateResponseTimes 
     - Event: Time-driven
     - Type: Day timer
       -- Time: 6 am to 7 am

 #### 4.3: Data Validation & Quality Checks   
 #### Tasks:
 #### 1. Created a Data Quality Dashboard in a new sheet called "Data_Quality".
 #### 2. Created Data Validation Rules
  - Applied data validation to critical fields
  - Set up conditional formatting for data quality alerts
  - Created dropdown lists where applicable
  #### 3. Test Data Integrity
  - Submitted some test FTA forms
  - Submitted corresponding feedback forms
  - Verified that all metrics were calculated correctly
  - Check for any formula errors
  #### WEEK 4: Looker Studio Dashboard Development
  #### Objectives:
  #### 5.1. Looker Studio Setup & Data Connection
  #### Tasks:
  #### 1. Created Looker Studio Report
  - went to lookerstudio.google.com
  - Clicked "Create" → "Report."
  - Named: "TSP A-Team Performance Dashboard"
  #### 2. Connected Data Sources
  - Added data source: Google Sheets
  - Selected "A-Team Master Data" spreadsheet
  - Added the following sheets as separate data sources:
   - ■ FTA_Responses
   - ■ Feedback_Responses
   - ■ Assignment_Log
   - ■ Dashboard_Metrics
   - ■ A-Team_Members
  #### 3. Configured Data Source Settings 
  - For FTA_Responses:
   - ■ Set "Timestamp" as Date type
   - ■ Set rating fields as Number type (Average
aggregation)
   - ■ Set FTA_ID as Text type
 - For Feedback_Responses:
   - ■ Set "Timestamp" as Date type
   - ■ Set FTA_ID as Text type (join key)
 #### 4. Created Blended Data Source  
 - Blended FTA_Responses with Assignment_Log 
 - Join key: FTA_ID
 - Join type: Left outer join
 - Included fields: FTA details + Assigned member info 
 #### 5.2: Dashboard Layout & Header Section
 #### Tasks: 
 #### 1. Set Up Dashboard Canvas
 - Canvas size: 1200px width (auto height)
 - Theme: Choose a professional color scheme (e.g., church brand colors)
 - Added church logo in top-left corner
 #### 2. Created Header Section
 - Added text: "The Standpoint Church - A-Team Performance Dashboard."
 - Font: 24pt, Bold
 - Added date range selector (top-right)
 - Added last refresh timestamp
 #### 3. Created KPI Scorecard Section (Row 1). Created scorecards for:
 - Total FTAs
     - ■ Data source: Dashboard_Metrics
     - ■ Metric: Total FTA value
     - ■ Showed comparison to the previous period
 - FTAs This Month
     - ■ Data source: Dashboard_Metrics
     - ■ Metric: FTAs This Month
     - ■ Showed trend sparkline
 - Average Experience Rating

    - ■ Data source: Dashboard_Metrics
    - ■ Metric: Avg Overall Experience
    - ■ Color scale: Red (<3), Yellow (3-4), Green (>4)
  - Membership Interest Rate
    - ■ Data source: Dashboard_Metrics
    - ■ Metric: Membership Interest Rate
    - ■ Style as percentage

#### Outcome and Summary
- All Google Sheets data was successfully connected to Looker Studio
- Data sources were properly configured and blended
- A professional, branded dashboard layout was created
- Key KPIs were clearly visualized using scorecards
- Interactivity was enabled through date range controls
- The dashboard was prepared for sharing with leadership and team coordinators
- This dashboard further served as a single source of truth for monitoring A-Team performance, improving follow-up processes, and supporting data-driven decisions at The Standpoint Church.


#### Screenshot of Data dictionary
<img width="911" height="552" alt="Image" src="https://github.com/user-attachments/assets/9806e847-2933-472a-bc09-1a1f967f75f3" />


#### Screenshot of TSP dashboard
<img width="1011" height="753" alt="Image" src="https://github.com/user-attachments/assets/5c5a0723-54f1-4955-bc42-4d3002cdf2d2" />




#### Link to the TSP_ Response Form
https://docs.google.com/forms/d/e/1FAIpQLSeyOcm4neTpX9AK49w07qLIRB4Jd-shiDikIBFnBoX2ftImKg/viewform?usp=header


#### Link to the TSP _Feedback Form
https://docs.google.com/forms/d/e/1FAIpQLSf5mUsEjOqX5Y9HYLFZtYJMulQYG9BvLKR4v4taTDNWv5NaKQ/viewform?usp=header












