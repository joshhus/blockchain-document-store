---

copyright:
  years: 2018
lastupdated: "2018-11-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Authorize the service

Once you have configured the **Blockchain Document Store** service, you will
authorize the service on your network channel peers.

Complete the following steps to authorize the service:  

1. **Copy certificate**:
Log in to your [IBM Cloud Resource Dashboard ![External link
icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){:new_window} and select your instance of the Blockchain Document
Store service, at *service-onboarding-basepath*/onboarding. Copy your organization's
displayed service certificate, which will be similar to the following example:

    ```
-----BEGIN CERTIFICATE-----
AAAAA3NzbC3yc2RGWRHSEGWEGSEGAQDXIl5aasdfasdgj7nNt/xDESGWWE8CqGf25sdgxiNABzSDGSEG248362K5ArKFXgrTt0tXvQsUZqmOYRVwiITgySG97097SGSGoGsJbDMPZH4kRnHS6wqjyQ6qQ/eB7G4WTNBCSLtRadiBadg086SG06agawerg96089578olGYqrmy/kB/1JdS+TPkGr1vdabwwAVo7SHSEGSEF086086985sfxy+upnalERAQi2aF2STap2Bj9hoGPjsesegsegsegId/gzlDyS8lsYSEGSEG0869859D0XnlcQeBow3dvTlbvBWAsDO2QMVR+UcHD8hrroRSEjSGSEG89697587445609SGSEEEGGSGEqxMJByiAjI9JED9rl/lDWGeIJuPYl==
-----END CERTIFICATE-----
    ```

2. **Add certificate**: From your [IBM Cloud Resource Dashboard ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){:new_window} select your IBM Blockchain
Platform network resource. Then select the **Manage** tab, and click the **Enter Monitor**
button in the content pane. Select **Members** from the navigation pane. In the content pane,
select the **Certificates** tab and click the **Add Certificate** button. In the
**Add certificate** dialog, paste your Blockchain Document Store certificate (which you
copied in the previous Step 1) in the **Certificate** field. Also enter a **Name** for the
certificate, and click **Submit** to add the certificate to your organization profile.

3. **Restart peers**: From your IBM Cloud Resource Dashboard, select **Overview**
in the navigation pane. Your IBM Blockchain Platform network
resources, including Orderer, CA (Certificate Authority), and Peers, will be displayed.
From the **Actions** menu on the right, click the stop icon for each **Peer**, and wait
for each peer status to change to **Stopped**. Then click the play
icon for each stopped peer, and wait for each peer status to change to **Running**.
This refreshes the Blockchain Document Store service certificate on each peer.
Note that if you do not do these peer restarts, you will have to restart your peers
manually before completing the authorization process.

4. **Sync certificate**: From your IBM Cloud Resource Dashboard, select **Channels**
in the navigation pane. The channel that you are provisioning Blockchain Document
Store to is displayed. For this channel, click the **Actions** menu on the right,
and select **Sync Certificate**. From the **Sync certificate** dialog, click
the **Submit** button.

5. **Complete authorization**: **Return** to the Dashboard for your Blockchain
Document Store instance, and click the **Done authorizing** button
to complete the service authorization process.

## What's next?
Proceed to [install and instantiate the service](install-instantiate-service.html).
