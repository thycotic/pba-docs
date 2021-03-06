[title]: # (Webhooks)
[tags]: # (secret server,administration,admin,aettings,notifications)
[priority]: # (6010)

# Webhooks

PBA integrates into external workflow and security systems via webhooks. A webhook is a user-defined callback which is executed in response to an event (alert or warning in PBA). Along with Access Challenges and email notifications, webhooks comprise the responsive actions in PBA in response to detection of anomalous activity.

## Configuration

### URL

This is the URL to which a POST request is sent when an event is created.

### Signing Secret

This is optional. If set, a header is set (x-hub-signature) with the SHA256 signature of the body of the email.

Example Signature Verification in Python 2.7:

```python
from Crypto.Hash import SHA256
from Flask import requests
\# receive the request
signature = request.headers.get('x-hub-signature',None)
payload = request.data.decode('utf-8')
hmac = SHA256.new(secret)
hmac.update(payload)
expected_signature = "sha256="+hash.hexdigest()
assert signature == expected_signature
```

### Encoding

Encoding may be set to either `application/json` or `application/x-www-form-urlencoded`.

However, only `application/json` supports mapped templates (customized `POST` body; see below).

### Custom Headers

This is optional. This field takes JSON formatted headers and adds them to the POST request. For example, to configure basic authentication with username **admin** and password **admin**, you would generate the base64 string of `username:password (admin:admin)` using the Python example code below, and then set the custom header field to:

```bash
{"Authorization" : "Basic YWRtaW46YWRtaW4="}
import base64
base64.b64encode("admin:admin")
\# output is: YWRtaW46YWRtaW4='
```

### Mapping Template

This is optional. The Mapping Template takes a string as an argument which will be used as the body of the POST. Before doing the POST, PBA will substitute any tokens specified in the mapping template with data from the event. Here are the supported tokens:

* `EventId`
* `UserId`
* `UserName`
* `UserEmail`
* `DisplayName`
* `StartDate`
* `EndDate`
* `RiskScore`
* `Interval`
* `Severity`
* `Threshold`
* `Hostname`

Note that in use, these are enclosed in @ signs, for example: @Severity@

All of the above tokens except `Hostname` are event fields. The `Hostname` token denotes the hostname of the PBA instance, and may be used to configure a link back to the PBA event from the system which receives the Webhook POST.

#### If Omitted

If the Mapping Template is not set, then the event (alert or warning) will be serialized and posted as either JSON or urlencoded form data.

* This out-of-the-box formatting of the POST body may be fine for integrating with custom‑built REST endpoints, but it is less useful for integrating directly with other products.
* As an example, see the configuration for [Creating an Incident with ServiceNow](#example__creating_an_incident_in_servicenow), below.

## Example: Creating a SlackBot

The full instructions for creating a Slack Webhook consumer are available here:

* <https://api.slack.com/incoming-webhooks>

In this example, we forward the PBA events to Slack and they are posted to a channel using a SlackBot in our specified format.

1. Navigate to <https://api.slack.com/apps> create a new app.
2. Turn on **Incoming Webhooks**.
3. Copy your Webhook URL.
4. Click on **Oauth & Permissions** and under **Scope \> Select Permission Scopes**, add **Post to a specific channel in Slack** for the channel to which you want the messages posted.
5. In PBA, enable Webhook, and paste the Webhook URL from Step 3 into the **URL** field.
6. Create a Mapping Template with a single JSON field, **text**, and set its value to the format you want the SlackBot to use. For example:

```json
{
"text":"PBA Alert: https://@Hostname@/handle_ub_alert/@EventId@\n
Secret Server User: @DisplayName@ (User ID:@UserId@)\n
Time Range: @StartDate@ - @EndDate@\n
Interval: @Interval@\n
Risk Score: @RiskScore@\n
Severity: @Severity@\n
Threshold: @Threshold@"
}
```

## Example: Creating an Incident in ServiceNow

The configuration displayed below is an example of Webhook settings that would create an incident in ServiceNow. Here is the Mapping Template:

```bash
{"assignment_group":"security",
"caller_id":"6816f79cc0a8016401c5a33be04be441",
"description":"Pba Alert\nSecret Server User: @UserName@ (UserId:@UserId@)\n
Pba Event: https://@Hostname@/eventdetails/@EventId@\n
Activity Start: @StartDate@\n
Activity End: @EndDate@\nInterval: @Interval@\n
Risk Score: @RiskScore@\nSeverity: @Severity@\n
Threshold: @Threshold@", "impact":"1",
"short_description":"PBA Alert on Secret Server User @UserName@. Risk Score: @RiskScore@",
"work_notes":"reported PBA alert"}
```

### Notes

Be aware that:

* ServiceNow's REST API uses basic authentication.
* The **caller_id** field should be set to the **id** of the ServiceNow service account used for authentication.
* Thycotic provides a callback link in the incident description:
    <https://@Hostname@/eventdetails/@EventId@>
  It is also possible to configure an html URL field in ServiceNow and format this as a proper anchor tag.
