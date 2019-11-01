[title]: # (PBA Operations)
[tags]: # (Privileged Behavior Analytics,PBA,)
[priority]: # (4090)

# User Details

The **User Details** page is the ideal place to dive deeper into a specific User’s behavior from the perspective of many types of data collected on them.

You can access User Details by navigating to **Details** > **Users**.

![alt](images/d96a839f41633fe8467fef229b39fdcb.jpg)

The User Details page lists all Users, their Display Names, Account Type, the number of unique Secrets they have accessed, the total number of times they have accessed Secrets, when they were first seen in Privileged Behavior Analytics, and when they were last active.

Click on a User name to open that User’s Details page, which shows:

![alt](images/83642134bd55207bfce0a117edbdf0b1.jpg)

* **User IP Address History**: lists any IP addresses they have accessed Secret Server from

![alt](images/82f06fc144498f335df0fbd155be046e.jpg)

* **Secret Activity**: lists the most recent 500 encrypted Secret accesses, when they occurred, the Secret IDs and names accessed, and how they were accessed

![alt](images/e264459ffade529228e1b69b7e26af20.jpg)

* **Secret Server Administrative Actions**: lists any administrative actions the User has performed in Secret Server, when it occurred, what the specific actions was, and if it affected any Secret Server Users

![alt](images/6e92ecbf33f6f1d8d64714966545ea70.jpg)

* **Activity Timeline**: a chart showing when a User has performed Secret accesses, Secret modifications, or administrative actions in Secret Server, or has logged in or out of Secret Server over time
  * each activity is denoted by a symbol shown in the legend at the top
  * placing your mouse over any of the symbols in the graph will give more details on what the user did at that time
  * grabbing and moving the side buttons on the bottom chart will zoom the top chart

![alt](images/2269ab3a3b4497789d5eff350dd397fd.jpg)

* **Most Frequent Secrets**: an animated representation of the top 20 most accessed Secrets by the User; you can zoom into the graph by scrolling, or right-click on any node or link to view more details

![alt](images/28800922f594efb413d412d924aac535.jpg)

* **Temporal Behavior**: a chart showing all temporal data for the User organized by time of day and day of the week
  * the numbers across the bottom indicate the total events involving the User for that time of day
  * the values across the right side indicate the number of events involving the User for that day of the week
  * the legend at the bottom shows the number of events that correlate to the coloring of the chart blocks
  * mouse over a block to get the total number of accesses for that day of week and hour of day