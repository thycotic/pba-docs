[title]: # (Architecture)
[tags]: # (Privileged Behavior Analytics,PBA,Overview,Architecture,Metadata)
[priority]: # (2010)

# Architecture

Privileged Behavior Analytics uses AWS internals to provide its features.

![Thycotic Privileged Behavior Analytics Cloud](images/architecture-simple.png)  

As in the illustration:

* Your Secret Server uploads its activity logs to PBA in the Cloud.
* PBA applies AWS-based algorithms to the data to deliver alerts, analytics, and visualizations.
* To access these, your administrative staff use a browser to authenticate with PBA.

