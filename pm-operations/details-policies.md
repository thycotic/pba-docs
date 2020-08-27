[title]: # (Policy Details)
[tags]: # (Privilege Manager,Privileged Behavior Analytics,PBA,Operations,Policy,Details)
[priority]: # (4600)

# Policy Details

The **Policy Details** page can be used to investigate policy activity from the perspective of many types of data collected on it.
You can access Policy Details by navigating to **(Privilege Manager Analytics)** > **Details** > **Policies**.

![Policy List](images/details-policies.png "Policy List")

The Policy Details page lists all policies and includes summary statistics and links to further details.  If you click on any of the policy names or IDs you will be directed to that entity’s details page, which shows the following:

* **Policy Stats**: lists key statistics such as total number of events, time range, and most active user

![Policy Statistics](images/details-policies-stats.png "Policy Statistics")

* **Activity Timeline**: shows all application access activity for the policy, including timestamp, endpoint, user, and IP address
  * mouse over a colored circle for details on a particular event
  * the chart can be panned left and right by dragging or zoomed by scrolling, which also filters data in the table

![Policy Activity](images/details-policies-activity.png "Policy Activity")

* **Temporal Behavior**: a chart showing all temporal data for the policy organized by hour of day and day of the week
  * the numbers across the bottom indicate the total events involving that policy for that hour of day
  * the values across the right side indicate the number of events involving that policy for that day of the week
  * the legend at the bottom shows the number of events that correlate to the coloring of the chart blocks
    * mouse over a block to get the total number of events for that day of week and hour of day

![Temporal Behavior](images/details-policies-temporal.png "Temporal Behavior")
