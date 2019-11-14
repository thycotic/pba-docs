[title]: # (Secret Details)
[tags]: # (Privileged Behavior Analytics,PBA,Operations,Secret Details)
[priority]: # (4110)

# Secret Details

The **Secret Details** page can be used to investigate how a Secret is being accessed from the perspective of many types of data collected on it.
You can access Secret Details by navigating to **Details** > **Secrets**.

![alt](images/25-secret-list.png)

The Secret Details page lists all Secrets with Secret ID, Secret Name, Secret Template, the total number of events (Secret accesses plus modifications), number of Distinct Users that have accessed the Secret, the Created date, and the date of Last Activity.

If you click on any of the Secret names you will be directed to that Secret’s Details page, which shows the following:

* **User Activity**: lists the most recent 500 encrypted accesses for the Secret, when they occurred, who accessed it, and how it was accessed.

![alt](images/26-secret-details-a.png)

**Activity Timeline**: shows all activity for the Secret, including alerts and warnings, accesses, and modifications as well as timestamps, IP address, and event details.

* mouse over a colored circle for details on a particular event
* the chart can be panned left and right by dragging or zoomed by scrolling, which also filter data in the table

![alt](images/27-secret-details-b.png)

* **Most Frequent Users**: an animated representation of the top 20 users accessing the Secret the most; you can zoom into the graph by scrolling or right-click on any node or link to view more details

![alt](images/28-secret-details-c.png)

* **Temporal Behavior**: a chart showing all temporal data for the Secret organized by time of day and day of the week
  * the numbers across the bottom indicate the total events involving that Secret for that time of day
  * the values across the right side indicate the number of events involving that Secret for that day of the week
  * the legend at the bottom shows the number of events that correlate to the coloring of the chart blocks
    * mouse over a block to get the total number of events for that day of week and hour of day

![alt](images/29-secret-details-d.png)

* **Secret Name and Folder History**: lists any changes that have been made to the name of the Secret or the folder it is kept in inside Secret Server

![alt](images/30-secret-details-e.png)
