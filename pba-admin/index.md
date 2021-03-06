[title]: # (PBA Administration)
[tags]: # (secret server,admin,settings)
[priority]: # (6000)

# PBA Administration

In PBA, most administrative tasks will occur on the **System Settings** page, which is used to set basic configurations for alert notifications and other general settings.

You can navigate to System Settings by clicking on the cogwheel symbol at the top right of any PBA page and choosing System Settings.

## Responsive Actions Settings

The **Responsive Actions** section of System Settings is used to configure PBA to take automated action based on user risk score.

![alt](images/resp-actions.jpg)

**Alert Threshold**: The numerical value an alert needs to meet or exceed to send an email and log the event on the Alerts page.

**Alert Action**: Provides three different automated actions that PBA can take in response to an Alert Event.

* The **Challenge** response can be configured to automatically impose additional controls on a Secret Server user if their actions cause PBA to generate an alert that meets or exceeds the Alert Threshold. The current version of PBA can challenge a user by
  * logging them out of Secret Server
  * forcing them to do 2-factor authentication
  * locking a user out of Secret Server
  * forcing them to request access to any Secrets they access
  Challenges must be configured on Secret Server as well.
  More information on how to configure Challenges can be found in [Getting Started](../getting-started/index.md).
* The **Webhook** response can be configured to integrate with external systems by sending an HTTP post when PBA has a user alert event. Additional information can be found in the [PBA Responsives](../pba-responsives/index.md) article.
* The **Code Hook** response can be configured to integrate with external systems by executing a user provided script when PBA has a user alert event. Additional information can be found in the [PBA Responsives](../pba-responsives/index.md) article.

**Warn Threshold**: The numerical value a warning needs to meet or exceed to send an email and log the event on the Alerts page.

**Warn Action**: Provides three different automated actions that PBA can take in response to an Alert Event. See the above *Alert Action* list item for details on automated actions.

**Test Actions**: Provides an ability to test Responsive Actions to ensure your configuration is correct.

**Secret Importance**: A page that lists all Secrets and enables changing any of their importance settings for PBA. More important Secrets are more likely to trigger alerts upon User access.

**User Watch List**: Configuration options to automatically populate the User Watch List with new users and/or users with active alerts and warnings.

## Secret Server Integration Settings

The **Secret Server Integration Settings** section is used to configure secure communications between your Secret Server and PBA.

![alt](images/ss-int-settings.jpg)

**Secret Server Integration Key**: A key that provides your Secret Server with credentials and configuration information to upload log data to PBA.

**Secret Server Public Key**: A one-time RSA public key is entered here to establish communication between Secret Server and PBA.

## Time Settings

The **Time Settings** section is used to configure the Timezone and time display format.

![alt](images/time-settings.jpg)

**Local Timezone**: The display of all timestamps can be adjusted to your local time zone. The default time zone is UTC.

**Hour Display**: 12-hour (AM/PM) or 24-hour (international or “military”) time display.

### User Settings

The **User Settings** section has password and alert preferences settings.

![alt](images/user-settings.jpg)

**Account Settings**: The link enables changing the password for the account used to access PBA.

**Alert Notification Settings**: Enables setting the email address for receiving alerts and whether you want to receive alerts or warnings as they occur.
