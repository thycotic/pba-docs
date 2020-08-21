[title]: # (Application Graph)
[tags]: # (Privilege Manager,Privileged Behavior Analytics,PBA,Operations,Application Graph)
[priority]: # (4520)

# Application Graph

The **Application Graph** can be used to explore the behaviors of Privilege Manager users and activity of applications, endpoints, and policies at a glance.

The graph is animated by default. You can pause the animation by clicking on the pause button at the top right of the graph area. Above the pause button is another button that will allow you to expand or collapse all nodes with a single click. You can also expand or collapse individual clusters by double clicking on them.

Each initial node circle, or Community, is a collection of users who are accessing similar applications. The larger the Community, the more users and applications there are inside it.

Communities may also have lines, or links, connecting them to other Communities. The links are an indication that a user or users within a Community are accessing applications that exist in another Community, indicating a possibility of accesses outside a User’s responsibility. Thicker links represent more accesses between Communities.

When you expand (double-click) a Community, you can see all the users and applications it contains. The size of each node indicates how many accesses it has and the thickness of links follows the same principal.

(Coming soon: Community, User, and application nodes may be outlined by a shade of red. If this is the case, there is an active alert for a user and/or application and more information can be found by right clicking on the affected nodes and observing active alerts or by navigating to the **Privileged Behavior Alerts** page.)

![Application Graph Overview](images/app-graph.png "Application Graph Overview")

Whether a Community is expanded or not, you can right click on any node or link on the Application Graph to add notes or see further details.

The icon to the left of the menu buttons will toggle the Graph between light and dark themes.

## Filters

The Filters menu (three horizontal lines button) provides options to limit the number of nodes and links displayed.

![alt](images/filters.jpg)

* **OR AND Filter**: determines how filters will be applied to the Graph
* **Filter by selected**: lets you filter the Graph display by Application, User, Endpoint, Group, IP Address (and City, Region, Country), or Policy
* **Time Ranges**: by default, the Graph will show activity from the last week; the Custom Range option allows selecting a start and end date to refine activity displayed
* **Save or select graph layout**: you may choose to save filtered views of the Graph to quickly recall significant access landscapes

## Notes

The Notes menu can be accessed by clicking the button depicting a note with a folded corner at the top right of the Application Graph page.

![alt](images/09-notes.png)

* All notes on nodes and links are listed here. You can edit any note by clicking on it or delete a note by clicking on the trashcan icon to the right of the note.
* Notes can be created by right-clicking on a node (circle) or link (line) in the Application Graph. A small square of the color selected will appear on the node or link after the note is created.
* Hovering over the square or a note in the Notes menu will briefly highlight the note square on the Graph.

## Table

The Table menu can be accessed by clicking the icon between the Notes and Tools buttons at the top right of the Application Graph page.

![alt](images/10-table.png)

This menu gives you a full, sortable text-based list of all User and Application node metrics. Placing your mouse over any of the node names in the lists will highlight that node on the Application Graph if the Community it is in is expanded.

* **Community** lists User and Application nodes and the Community number they are in
* **User/Application** lists User and Application node names and whether each is a User or Application
* **Number Connections** lists User and Application nodes and how many accesses they have had or performed on other nodes
* **Number Unique** lists User and Application nodes and how many unique applications or users, respectively, they are connected to
* **Last Active** lists User and Application nodes and the timestamp of the last activity each had
* **First Active** lists User and Application nodes and the timestamp of the first activity each had recorded in PBA
* **Social Network Metrics** lists User and Application nodes and the numerical value of the selected metric

## Tools

The Tools menu (cogwheel button) allows you to customize what is displayed on the Graph.

![alt](images/11-tools.png)

* **Search**: At the top of the menu is a search field where you can enter the name of a User or Application to highlight that specific node on the Application Graph. Press Enter to repeat the animation.
* **Alert Indicators**: turned on by default, this will outline nodes in a shade of red based on whether it has an active alert; the redder a node is the higher the total alert risk
* **Background Blobs**: turned on by default, these surround all nodes in an expanded Community with a color similar to that of the collapsed Community
* **Node Icons**: turned on by default, this shows icons in place of circles for each user or application node. The size of the icon can be changed using the **Large** switch.
* **Node Labels**: turned on by default, these are Community numbers, application names, and user names shown next to each node
* **Note Boxes**: turned on by default, these represent notes that have been placed on any nodes or links
* **Cluster/Expand by**: by default, all nodes will be clustered by Communities; you can select the dropdown here to choose to cluster nodes by applications and users
* **Node Color**: there are multiple options for choosing how the nodes within an expanded Community are colored:
  * **Community**: all Application and User nodes will be the color of the Community when it is collapsed
  * **User/Application**: the User nodes are colored blue and Application nodes are colored green (default coloring)
  * **Number Connections**: Application and User node colors will range from white to red; the redder a node is, the more active it is
  * **Number Unique**: Nodes will range from white to red, and the redder a node is, the more unique accesses it has
  * **Last Active**: Nodes will range from white to red with recent activity being more red
  * **First Active**: Nodes will range from white to red with earlier activity being more red
  * **Social Network Metrics**: these options can reveal important applications or users in the network
* **User Node Group Type**: Select a user type to change nodes to that metric (e.g. selecting Endpoint will show endpoint nodes connected to application nodes)
* **Application Node Group Type**: Select an application type to change nodes to that metric (e.g. selecting Policy will show user nodes connected to policy nodes)
