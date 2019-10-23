[title]: # (Release Notes)
[tags]: # (Privileged Behavior Analytics,PBA,)
[priority]: # (8000)

# Release Notes
 ## Privileged Behavior Analytics 3.1
Release Date: January 2019   Corresponds to Secret Server 10.6  Bug Fixes
* Bug fixes for IP address processing
## Privileged Behavior Analytics 3.0
Release Date: January 2019   Corresponds to Secret Server 10.6
Enhancements
* New IP Address Analytics that include:
* Map feature that visualizes Secret accesses by location
* Detailed reports of actions by IP address
* Searchable and filterable list of IP addresses, locations, and stats
New Administrator Action Analytic Suite that includes:
* Map to visualize Secret Server administrators’ actions by location
* Clock to visualize Secret Server administrators’ actions by time
* Graph to visualize links between Secret Server administrators and their actions
* Charts with filters to visualize the “Most Active Admins and Actions”
New Dashboard widgets for administrator actions and an IP address map
PBA Activity Log for internal auditing purposes
Several design, security, and speed improvements
## Release Notes 2.1.3
Release Date: September 2018   Corresponds to Secret Server 10.5
Analytics Improvements
* Graph Visualization - Added Node Icons, additional data available for each node, and various other small improvements.
* Data Clock Visualization - Improved filter options and ability to link into filtered views.
* Most-Active Analytics - Swapped out library for cohesive feel with Dashboard.
* Details Timeline Analytics - Updated library for better visualization and data filtering.
Usability Improvements
* Alerts indicator is now displayed on all pages.
* Improved the layout on the Alerts page.
* Details Pages - Added a stats card to display a summary of User & Secret activity on each corresponding Details page.
## Release Notes 2.0.2
Release Date: March 2018   Corresponds to Secret Server 10.4  Enhancements
* User Watch List
    * Added a User Watch List page to help admins keep a closer eye on key     users and provide a centralized starting point to dive into analytics.     By default, the Watch List automatically adds users with open alerts or     warnings as well as new users.
    * Can manually add users to User Watch List with customizable notes and     "reasons" (e.g. "Departing User, Suspicious"). To enable quick action,     each user's entry includes links to their PBA Details' page, Active     Alerts, and the Secret Server User Edit page.
* Webhook Response Actions
    * PBA can now send alert data to a web endpoint, such as ServiceNow or     Slack, to make responding to an alert easier. PBA can also run a script     to execute additional actions not possible with a webhook. For example,     a codehook can be configured in PBA to take actions (e.g. locking     accounts of a user with suspicious activity) in any combination of     systems including Human Resources, Security, Identity, or Workflow.
* Email Enhancements
    * Redesigned Alert Emails to include details of each alert or warning     along with links to take immediate action like “Investigate,” “Dismiss,”     or “View User Activity.”
    * The PBA alerting system can now trigger faster alerts, so admins will     know within moments whether a user is acting out of the ordinary.
* UI Updates
    * User and Secret Details' pages are enhanced with new statistics boxes     that show key information and action links.
## Release Notes 1.1.0 -------------------
Release Date: November 2017   Corresponds to Secret Server 10.4  Enhancements
* Secret Server can act as an identity provider for Privileged Behavior Analytics. Any user with the View Security Analytics role permission in Secret Server may log into Privileged Behavior Analytics. Additionally, any user with Administer Security Analytics role permission is able to perform administrative actions once logged into Privileged Behavior Analytics through Single Sign-On (SSO). Local Privileged Behavior Analytics users (the initial users prior to integrating Privileged Behavior Analytics into Secret Server) still have administrative rights as well.
* Privileged Behavior Analytics can now integrate with Secret Server Cloud.
* Privileged Behavior Analytics’ Dashboard now has a Dashboard Assistant, a feed of the important events that have occurred in a customer’s Secret Server environment that details why those events are important to see and what should be done as a result.
* Privileged Behavior Analytics has integrated with AppCues to provide useful product tours throughout each page.
* Secret Access Graph Enhancements
    * Nodes on the Secret Access Graph are now outlined by varying shades of     red if there is an active alert affecting them.
    * Filter configurations can now be saved and recalled for convenient views     of the Secret Access Graph.
