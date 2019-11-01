[title]: # (PBA Responsive Actions)
[tags]: # (Privileged Behavior Analytics,PBA,Responsive Actions)
[priority]: # (5000)

# PBA Responsive Actions

In Privileged Behavior Analytics, anomalous behavior is characterized as an event and assigned a risk level. If this risk level exceeds a pre-defined threshold, the following response actions may be used to triage the potential threat:

* Notification Actions
  * Email Notifications
* Dynamic Actions
  * Access Challenges
  * Webhooks
  * Codehooks

## Email Notifications

Each PBA user may set an email and choose to be notified when an event occurs. Upon receipt of an email notification, the anomalous activity should be investigated and remediated if necessary.

## Access Challenges

Access Challenges provide automated responses in Secret Server to PBA events.

* Access Challenges allow for the dynamic configuration of the trust level in the Secret Access Workflow which is built into Secret Server.
  * For example, it may be infeasible to configure Session Recording on every Secret (disk space and CPU limitations) and it may be considered onerous to configure the Approval workflow on every Secret (administrators become desensitized to approving access to every single request).
    With Access Challenges, however, these workflows can be enabled dynamically when a user’s behavior has become suspicious, helping to ease the tension operationally between security and efficiency.

An expiration duration may be specified for the Challenge, or the Challenge may be valid indefinitely.

* For the **Login** and **Two Factor** Challenges, the challenged user may clear the Challenge by re-authenticating.
* For the other Challenge types, a Secret Server user with PBA permissions must clear the Challenge for the user, or the user must wait for expiration.
  For example, a **Requires Approval** Challenge may be configured with a two-hour expiration. This gives the security team a buffer of time to investigate the anomalous activity, while allowing the user to still access their usual Secrets, but in a more restricted workflow.

### Challenges in Version 10.2.000000 and Later

**Login**: User must re-authenticate with Secret Server.

### Challenges in Version 10.3.000015 and Later

**Two Factor**: User must re-authenticate with Secret Server and the Two Factor Remember Me is expired if set.
**Require Approval**: User must request approval for accessing any secrets unless they are the only Approver for that secret.
**Lockout**: User is locked out from Secret Server. This may be configured to include Secret Servers that use SAML and integrated authentication.

### Challenges in Version 10.4.00000X and Later

**Session Recording**: User has their sessions recorded for any secrets that are capable of session recording.

* This session recording is surreptitious, and there is no indicator to the user that they are being recorded.

## Webhook

The Webhook action HTTP posts the metadata associated with the anomalous activity event (the user, the time, the actions or secrets accessed) to a user-defined HTTP endpoint.

The Webhook provides the capability to integrate PBA events into many other workflow and security systems. Examples include sending a message to a messaging application such as Slack or creating a case in a ticketing system like ServiceNow.

See the PBA Administration Section’s [Webhooks](../pba-admin/webhooks.md) article for more about Webhooks.

## Codehook

Codehooks allow integration with external workflow and security systems where a Webhook is insufficient for the desired behavior. They are user-defined scripts that execute in response to the anomalous activity event.

* Currently Python 2.7 scripts are supported, and Node.js support will be added in a future release.

An example of a Codehook response action is suspending the user’s Okta account. This action cannot be achieved by a simple Webhook, despite Okta’s REST API, because it requires a two-step process of looking up the user by email, and then using the user’s internal Okta identifier to suspend the account.

See the PBA Administration Section’s [Codehooks](../pba-admin/codehooks.md) article for more about Codehooks.
