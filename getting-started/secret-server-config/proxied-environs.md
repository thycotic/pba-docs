[title]: # (Proxied Environments)
[tags]: # (Privileged Behavior Analytics,PBA,Proxied Environments)
[priority]: # (3040)

# Proxied Environments

If your Secret Server has outbound access through a proxy, its **web.config** must be modified to specify the proxy configuration.

* If Secret Server is also clustered and has multiple worker roles enabled (see the [Background Worker](bkground-worker-clust-env.md) article), the web.config must be updated for each Secret Server in the cluster.
  Microsoft has [more information](https://docs.microsoft.com/en-us/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings) on this.

The other option in a clustered environment is to specify a remote site for the data upload, and upload data through a Distributed Engine. If the distributed engine’s host server is also behind a proxy, however, the engine’s **Thycotic.DistributedEngine.Service.exe.config** must be modified similarly to the **web.config** in order to specify the proxy settings.

* For Secret Server v10.4 or later, the **web-proxy.config** can be uncommented and updated to specify the proxy settings.
* For Secret Server v10.3.000015 or earlier, you must add proxy-related XML to the **web.config** file immediately following the file’s closing **\</configSections\>** tag, as depicted here:

```BASH
</CONFIGSECTIONS>
    <SYSTEM.NET>
        <DEFAULTPROXY ENABLED="TRUE" USEDEFAULTCREDENTIALS="TRUE">
             <PROXY USESYSTEMDEFAULT="FALSE" PROXYADDRESS="HTTPS://PROXY:PORT" BYPASSONLOCAL="TRUE"/>
        </DEFAULTPROXY>
    </SYSTEM.NET>
<CONFIGURATION TYPE="THYCOTIC.FOUNDATION.CONFIGURATION, THYCOTIC.FOUNDATION">
```
