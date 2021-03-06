[title]: # (Codehooks)
[tags]: # (secret server,administration,admin,settings,notifications)
[priority]: # (6020)

# Codehooks

PBA integrates into external workflow and security systems via **Codehooks**. A Codehook is a user-defined script which is executed in response to an event (alert or warning in PBA).

Along with Access Challenges, Email Notifications and Webhooks, Codehooks comprise the responsive actions in PBA to detection of anomalous activity. A Codehook has the same use case as a Webhook, but is used for an integration which requires more than just an HTTP POST request.

## Configuration

The **Script Template** is the script that will be executed as a hook in response to a PBA event.

* It must be written in Python 2.7, and use the pip packages [listed here](https://gist.github.com/gene1wood/4a052f39490fae00e0c3).
* If an unsupported pip package is needed by the script, contact Thycotic Support to request that it be added.
* Each script invocation has a 30 second timeout.
* Any files added to /tmp should also be removed when finished (i.e. os.remove('path_to_file')).
* Before executing the script, PBA will substitute any tokens specified in the mapping template with data from the event. Here are the supported tokens:
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
* All of the above tokens except `Hostname` are event fields. `Hostname` denotes the hostname of the PBA instance, and may be used to configure a link back to the PBA event from the system targeted by the Code Hook.

## Example: Suspending an Okta User Account

The script template displayed below is an example of a C script that looks up an Okta user by email (UserEmail token) and suspends the user. This example would be the equivalent of a Lockout Challenge in Secret Server, but extrapolated to an external system (Okta). Other potential C actions in Okta would include resetting a user's password or security questions.

```C
import urllib2
import urllib
import json
opener = urllib2.build_opener()
user = '@UserEmail@'
opener.addheaders = [('Authorization', 'SSWS <BASE 64 TOKEN>')]
response_str = opener.open('https://<OKTA URL>/api/v1/users?q={0}'.format(user))
response = json.loads(response_str.read())
body = response[0]
user_id = body.get('id',None)
if not user_id:
    print('user not found')
else:
    # suspend user
    url = 'https://<OKT ULR>/api/v1/users/{0}/lifecycle/suspend'.format(user_id)

    handler = urllib2.HTTPHandler()
    opener = urllib2.build_opener(handler)

    data = urllib.urlencode({})
    request = urllib2.Request(url, data=data)
    request.add_header('Authorization', 'SSWS <BASE 64 TOKEN>')
    request.get_method = lambda: "POST"

    try:
        connection = opener.open(request)
        except urllib2.HTTPError,e:
        connection = e

    if connection.code == 200:
        data = connection.read()
        print('Successfully suspended user: {}'.format(user))
    else:
        print('Failed to suspend user: {}'.format(user))
```

## Example: Fax Alerts

PBA supports Fax notifications via codehooks. Codehooks are user-defined scripts that are executed in response to an event (alert or warning in PBA). In this example on configuring Fax Alerts, we use a third-party service, [InterFAX](https://www.interfax.net/en), which is an online Fax service with an excellent API.

### Configuration

Below is the script that uses the **xhtml2pdf** Python library to convert an HTML document into a PDF for the Fax.

Make sure to replace your InterFAX API credentials and Fax number in the script below, and also to modify the Fax document header in the HTML template with your company and contact information.

(Note: Remember to remove files stored in /tmp when you are finished.)

```bash
from interfax import InterFAX
import os
import shutil
from uuid import uuid4
from xhtml2pdf import pisa
from cStringIO import StringIO
filename = "alert-fax{}.pdf".format(uuid4())
filepath = "/tmp/" + filename

fax_html = """<html><head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=8">
<title>bcl_1363603926.htm</title>
<meta name="generator" content="BCL easyConverter SDK 5.0.08">
<style type="text/css">

body {margin-top: 0px;margin-left: 0px;}

#page_1 {position:relative; overflow: hidden;margin: 102px 0px 174px 120px;padding: 0px;border: none;width: 696px;}
@page {
 size: a4 portrait;
 @frame header_frame { /* Static Frame */
 -pdf-frame-content: header_content;
 left: 50pt; width: 512pt; top: 50pt; height: 40pt;
 }
 @frame content_frame { /* Content Frame */
 left: 50pt; width: 512pt; top: 90pt; height: 632pt;
 }
 @frame footer_frame { /* Another static Frame */
 -pdf-frame-content: footer_content;
 left: 50pt; width: 512pt; top: 722pt; height: 150px;
 }
 }

.ft0{font: bold 19px 'Times New Roman';line-height: 22px;}
.ft1{font: bold 14px 'Times New Roman';line-height: 14px;}
.ft2{font: 15px 'Times New Roman';line-height: 17px;}
.ft3{font: bold 14px 'Times New Roman';line-height: 17px;}
.ft4{font: 1px 'Times New Roman';line-height: 1px;}
.ft5{font: bold 16px 'Times New Roman';line-height: 19px;}
.ft6{font: 16px 'Times New Roman';line-height: 19px;}
.ft7{font: 13px 'Times New Roman';line-height: 15px;}

.p0{text-align: left;padding-left: 150px;margin-top: 0px;margin-bottom: 0px;}
.p1{text-align: left;padding-left: 180px;margin-top: 49px;margin-bottom: 0px;}
.p2{text-align: left;margin-top: 0px;margin-bottom: 0px;white-space: nowrap;}

.td0{padding: 0px;margin: 0px;width: 384px;vertical-align: bottom;}
.td1{padding: 0px;margin: 0px;width: 54px;vertical-align: bottom;}

.tr0{height: 26px;}
.tr1{height: 31px;}
.tr2{height: 33px;}

.t0{width: 438px;margin-top: 42px;font: bold 15px 'Times New Roman';}

</style>
</head>
<body>
<div id="header_frame">
<p class="p0 ft0">Privileged Behavior Analytics Alert</p>
<p class="p1 ft1">{AMBARCO IT DEPARTMENT}</p>
<table cellpadding="0" cellspacing="0" class="t0">
<tbody><tr>
	<td class="tr0 td0"><p class="p2 ft1">DATE: %s</p></td>
	<td class="tr0 td1"><p class="p2 ft1">TIME: %s</p></td>
</tr><tr>
	<td class="tr1 td0"><p class="p2 ft1">TO: %s</p></td>
	<td class="tr1 td1"><p class="p2 ft1"></p></td>
</tr><tr>
	<td class="tr2 td0"><p class="p2 ft1">FROM: %s</p></td>
	<td class="tr2 td1"><p class="p2 ft1"><span class="ft2"></p></td>
</tr><tr>
	<td class="tr2 td0"><p class="p2 ft1">PHONE: %s</p></td>
	<td class="tr2 td1"><p class="p2 ft3">EMAIL: %s</p></td>
</tr><tr>
	<td class="tr2 td0"><p class="p2 ft1">Number Pages: 1</p></td>
	<td class="tr2 td1"><p class="p2 ft4">&nbsp;</p></td>
</tr>
</tbody></table>
</div><br>
<div id="content_frame">
<p class="p3 ft5">MESSAGE:</p>
<p class="ft1">Secret Server User: @UserName@ (UserId:@UserId@)</p>
<p class="ft1">Pba Event: https://@Hostname@/eventdetails/@EventId@</p>
<p class="ft1">Activity Start: @StartDate@</p>
<p class="ft1">Activity End: @EndDate@</p>
<p class="ft1">Interval: @Interval@</p>
<p class="ft1">Risk Score: @RiskScore@</p>
<p class="ft1">Severity: @Severity@</p>
<p class="ft1">Threshold: @Threshold@</p>
</span>
</div>
<div id="footer_content">
<p class="p5 ft5">DISCLAIMER:</p>
<p class="p6 ft7">The information contained in this fax is confidential and property of Ambarco Inc. Please do not distribute outside the organization.</p>
<p class="p7 ft7">Please check that you have received all pages per the page number above.</p>
</div>
</body></html>"""

to_name = "Security Administrator"
from_name = "Pba Service Account"
from_phone = "+1 669-221-6251 "
from_email = "pbaalerts@ambarco.com"
event_date, event_time = "@StartDate@".split('T')
event_time = event_time[:8]

formatted_fax_html = fax_html % (event_date, event_time, to_name, from_name, from_phone, from_email)

pdf = StringIO()
pisa.CreatePDF(StringIO(formatted_fax_html.encode('utf-8')), pdf)
resp = pdf.getvalue()

with open(filepath, 'w') as fd:
    pdf.seek(0)
    shutil.copyfileobj(pdf, fd)
interfax = InterFAX(username="<API USERNAME>", password="<API PASSWORD>")
fax = interfax.deliver(fax_number="+99999990", files=[filepath])
fax = fax.reload()    # resync with API to get latest status
print('Status:', str(fax.status), '  (Success if 0. Pending if < 0. Error if > 0)')
os.remove(filepath)   # remove pdf from /tmp
```
