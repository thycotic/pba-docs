[title]: # (Privileged Behavior Alerts)
[tags]: # (Privileged Behavior Analytics,PBA,Operations,Alerts,Severity,Score,Range,Admin Actions,Temporal Behavior,Historical Behavior)
[priority]: # (4030)

# Privileged Behavior Alerts

The Privileged Behavior Alerts page (**Alerts** > **Privileged Behavior Alerts**) displays events in Secret Server that do not align with normally observed behaviors. This includes the capacity to display Alerts for circumstances you define (see the [PBA Administration](../pba-admin/index.md) article).

![alt](images/c48c270d52123a15e22efbc9ca86ac64.jpg)

Use the search field to locate specific Alerts by searching on text from any of the rows in the table. Columns include:

* **Severity**: whether the event justified an Alert (serious event) or a Warning (minor event)
* **Score**: the numerical score given to the event depending on its severity and the severity of incorporated events
* **User**: the Secret Server User who caused the Alert; clicking their name opens the **User Details** page
* **Range of Activity**: the time span within which the Alert occurred
* **Secret Accesses**: any Secrets accessed during the time span of the Alert that contributed to the Alert; clicking on the Secrets opens the **Secret Details** page
* **Admin Actions**: any administrative actions taken in Secret Server during the time span of the Alert that may have contributed to the Alert; clicking on the Admin Actions listed displays the table of all administrative activity for that User
* **Temporal Behavior**: a time entry will be listed here if the Alert occurred at a time the User does not normally access the Secrets involved in the Alert; clicking on the time entry will display the User’s Temporal Data.
* **State**: indicates whether the Alert remains Active; the Clear button removes the Alert, adding it to the Historical Behavior Alerts archive
  * To further investigate the Alert, log actions you have taken on the Alert, adjust the importance of any involved Secrets, or provide feedback to Thycotic on the usefulness of the Alert, click **Actions**

![alt](images/081e1b426ddc072b61db893c5a23afe7.jpg)

## Historical Behavior Alerts

The Historical Behavior Alerts page archives Alerts after they have been cleared from an Active state.

You can reach the Historical Behavior Alerts by navigating to **Alerts** > **Historical Behavior Alerts**.

![alt](images/10e90a0b8cc27187a104410c2c2cb51e.jpg)

In viewing Historical Behavior Alerts, note these fields:

* **State Changed by**: the PBA User who cleared the Alert
* **Notes**: notes left on the Alert before it was cleared
