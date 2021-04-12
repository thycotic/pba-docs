[title]: # (Secret Server Configuration)
[tags]: # (secret server,data,metadata,uploader)
[priority]: # (3020)

# Secret Server Configuration
Steps to configure Secret Server with PBA:

1. Setup the [Data Uploader](data-uploader-setup.md). The Data Uploader provides data from Secret Server to PBA and is version-dependent.
1. Configure PBA for [Proxied Environments](proxied-environs.md) if your Secret Server has outbound access through a proxy.
Secret Server provides data to Privileged Behavior Analytics through the **Data Uploader**, which requires version-dependent configuration.
1. Import [Historical Data](historical-data-import.md) for PBA to analyze.
1. Set up the [Background Worker](bkground-worker-clust-env.md) for clustered environments.
