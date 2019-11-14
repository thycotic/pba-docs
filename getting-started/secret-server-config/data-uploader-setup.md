[title]: # (Data Uploader Setup)
[tags]: # (Privileged Behavior Analytics,PBA,Data Uploader)
[priority]: # (3030)

# Data Uploader Setup Steps

The Data Uploader setup steps depend on your Secret Server version.

## Version 10.3.000015 and Earlier

Privileged Behavior Analytics (PBA) processes event data from Secret Server using a data upload.

First obtain the Integration Key from PBA that will be used by Secret Server to authenticate with and upload data to PBA.

Log in to your PBA instance and navigate to **\<PBA\>/system_settings.** Click on **View Integration Key** and copy this key.

If you are prompted whether Secret Server is on version 10.4.000000 or later, click *No*.

![alt](images/01-data-uploader.png)

After copying the integration key, open Secret Server and navigate to **Administration > Privileged Behavior Analytics**. You should see the following screen:

![alt](images/pba-challenge-enabled.jpg)

Click **Edit**.

On the next screen, you will enter your PBA key in the field so named.

The PBA Key contains the secret access key and other parameters for uploading data to Thycotic PBA.

The key is encrypted for protection in transit. When you enter the key into Secret Server, it is encrypted and saved using your standard Secret Server encryption (AES-256 and DPAPI/HSM if configured).

The key can never be loaded again through the UI, but can be updated in case the linked Thycotic PBA account needs to be changed.

![alt](images/local-log-dir.jpg)

You will also need to specify the following fields:

**Enabled**: Enable Privileged Behavior Analytics.

**Site**: Set to Local by default, this will process and upload event logs using your IIS server running Secret Server (the default for your local site).

* If you are also using **Distributed Engine** you can specify a remote site and upload event data to PBA via Engines. This option is useful if you want to offload the work or if you prefer to allow an outbound firewall rule to the PBA servers from an Engine rather than from the server running Secret Server.

**Local Log Directory**: Event logs are stored on a local drive or network drive before being uploaded to cloud storage. Secret Server or your Distributed Engines (depending on whether you specify a local or remote site in the previous setting) must have write access to this local directory or network drive location.

* *IMPORTANT FOR CLUSTERED ENVIRONMENTS:* This setting is the same for all IIS nodes or engines on a given site. Therefore:
  * If you enable background worker on multiple web nodes (see the [Background Worker](bkground-worker-clust-env.md) article) and specify `C:\logs\uba` then you will need to create this same directory on each of your web node servers and ensure each Secret Server installation (web node) can write to its respective local directory.
  * The same applies to a remote site with more than one distributed engine; each of the distributed engine’s host machines must have a directory by this name, or have access to the network share if used.

**Challenge Enabled**: Enable Secret Server Access Challenges. See [Access Challenges](../access-challenges.md) for further information.

**Encrypt (At Rest)**: Encrypt event logs at rest in cloud storage. This is enabled by default and the recommendation is to keep it enabled. Performance improvements from disabling it are negligible.

**External PBA URL**: This is the URL of your Privileged Behavior Analytics cloud instance. It must be set manually and will change the PBA links in the Tools menu and Setup Home page to direct to your cloud instance in a new tab, instead of directing to this configuration page in Secret Server.

Setting this to your PBA URL will also convert the **PBA Event Id** column on the **Access Challenges** page to clickable links (see [Access Challenges](../access-challenges.md) for further information).

**Upload Frequency—Event Logs**: The frequency that event logs are uploaded to PBA. The recommend interval is 5 minutes. The minimum interval is 2 minutes.

**Upload Frequency—Metadata Logs**: The frequency that metadata is uploaded to PBA. The recommended interval is at least 60 minutes. The minimum interval is 5 minutes. Metadata frequency should vary based on how often new Users and Secrets are added in Secret Server, typically it should not need to be less than 60 minutes.

**Upload Frequency—Size Threshold**: You may also specify a maximum size threshold that will trigger an early upload before the temporal threshold (in minutes) is met. Because event logs and metadata are compressed prior to upload, the size threshold will not frequently be met (it safeguards against accumulating too many logs and experiencing processing delays).

**Local Retention**: This is the number of days that your event logs and metadata are stored in the local log directory specified.

* All historic event logs are maintained in the PBA database until account deletion.

It is good practice to set this threshold to at least 7 days, because if there is a connectivity issue between Secret Server and PBA, any event logs younger than the **Local Retention** setting will be uploaded upon re-connection.

When the configuration is saved and PBA is set to enabled, the configuration is validated. It can also be manually validated by clicking **Test PBA Key**.

## Version 10.4.000000 and Later, and Cloud

For Secret Server Installed Version 10.4 and for Secret Server Cloud, event data is uploaded to PBA via queues and micro-loading, and is closer to real-time. Prior versions of Secret Server data upload followed the more typical data warehouse design of file upload and small batch-loading.

### Special Case: PBA Already Enabled

If PBA was already enabled in Secret Server prior to upgrading to version 10.4.000000 or later, you must copy the integration key from PBA to Secret Server in order to enable Single Sign On.

Single Sign On requires a key exchange in order for PBA to use Secret Server as an identity provider, and a new integration key is provided with PBA’s public key in order to initiate this key exchange.

Use these steps to obtain the Integration Key from PBA that will be used by Secret Server to authenticate and upload data to PBA.

* Log into your PBA instance and navigate to **System Settings**.
* Click on **View Integration Key**.
* Copy the key.
  * If you are prompted to specify whether Secret Server is on version 10.4.000000, click *Yes.*

![alt](images/integration-settings.jpg)

* After copying the integration key, open Secret Server and navigate to **Administration > Privileged Behavior Analytics**. You should see the following screen.

![alt](images/confirm-ss-key.jpg)

* Click **Edit**.
* Enter your PBA key in the same-named field.
  * The **PBA Key** field contains the secret access key and other parameters for uploading data to PBA.
  * The key is encrypted for protection in transit; when you enter the key into Secret Server, it is encrypted and saved using your standard Secret Server encryption (AES-256, and DPAPI/HSM if configured).
  * The key can never be loaded again through the UI, but can be updated in case the linked Thycotic PBA account needs to be changed.
* Set the value for these fields:
  * **Enabled**: Enable Privileged Behavior Analytics.
  * **Site**: Set to Local by default, this will process and upload event logs using your IIS server running Secret Server (the default for your local site).
    * If you are also using Distributed Engine you can specify a remote site and upload event data to PBA via Engines. This option is useful if you want to offload the work or if you prefer to allow an outbound firewall rule to the PBA servers from an Engine rather than from the server running Secret Server.
* **Challenge Enabled**: Enable Secret Server Access Challenges. See the [Access Challenges](../access-challenges.md) article for further information. You may also click on **Advanced** to change additional settings:

![alt](images/pba-int-key.jpg)

**External PBA URL**: This is the URL of your Privileged Behavior Analytics cloud instance. It is set automatically by the integration key but may be overridden. This URL is used for Single Sign On, for redirecting to PBA from the Tools menu, and on the **Access Challenge** page to create links to the PBA events that spawned Access Challenges. See the [Access Challenge](../access-challenge.md) article for further information.

**Metadata Interval (Installed Only)**: The frequency that metadata is uploaded to PBA. The recommended interval is at least 60 minutes. The minimum interval is 5 minutes. Metadata frequency should vary based on how often new Users and Secrets are added in Secret Server; typically it should not need to be less than 60 minutes.

* For Cloud, this setting is unavailable and defaults to 60 minutes.

When the configuration is saved and PBA is set to enabled, the configuration is validated. It can also be manually validated by clicking **Test PBA Key**.
