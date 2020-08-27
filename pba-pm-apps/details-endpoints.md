[title]: # (Endpoint Details)
[tags]: # (privilege manager)
[priority]: # (4590)

# Endpoint Details

The **Endpoint Details** page can be used to investigate endpoint activity from the perspective of many types of data collected on it.
You can access Endpoint Details by navigating to **(Privilege Manager Analytics)** > **Details** > **Endpoints**.

![Endpoint List](images/details-endpoints.png "Endpoint List")

The Endpoint Details page lists all endpoints and includes summary statistics and links to further details.  If you click on any of the endpoint names or IDs you will be directed to that entity’s details page, which shows the following:

* **Endpoint Stats**: lists key statistics such as total number of events, time range, and most active user

![Endpoint Statistics](images/details-endpoints-stats.png "Endpoint Statistics")

* **Activity Timeline**: shows all application access activity for the endpoint, including timestamp, policy, user, and IP address
  * mouse over a colored circle for details on a particular event
  * the chart can be panned left and right by dragging or zoomed by scrolling, which also filters data in the table

![Endpoint Activity](images/details-endpoints-activity.png "Endpoint Activity")

* **Temporal Behavior**: a chart showing all temporal data for the endpoint organized by hour of day and day of the week
  * the numbers across the bottom indicate the total events involving that endpoint for that hour of day
  * the values across the right side indicate the number of events involving that endpoint for that day of the week
  * the legend at the bottom shows the number of events that correlate to the coloring of the chart blocks
    * mouse over a block to get the total number of events for that day of week and hour of day

![Temporal Behavior](images/details-endpoints-temporal.png "Temporal Behavior")

* **IP Address History**: a table of locations, total number of events, and time range of each IP address the endpoint was active on

![IP Address History](images/details-endpoints-ipaddress.png "IP Address History")
