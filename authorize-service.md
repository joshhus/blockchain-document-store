---

copyright:
  years: 2018
lastupdated: "2018-04-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Authorize the service
Once your organization has configured the IBM Blockchain Document Store service,
your Network Administrator will continue provisioning the service by authorizing
the service on your network channel peers.

**Authority/Role**: Network Administrator

To authorize your instance of the IBM Blockchain Document Store service on your
channel peers, your Network Administrator will use the IBM Cloud Service Dashboard
for your organization, at *service-onboarding-basepath*/onboarding.
**Note**: The *service-onboarding-basepath* is unique per organization; see your
blockchain network service provider.  

## Authorize service procedure
Complete the following steps to authorize the service:  

1. **Copy certificate**:
Log in to your instance of the Blockchain Document Store service, at *service-onboarding-basepath*/onboarding, and copy your **Network
Administrator Certificate**, which will be similar to the following example:

    ```
-----BEGIN CERTIFICATE-----
AAAAA3NzbC3yc2RGWRHSEGWEGSEGAQDXIl5aasdfasdgj7nNt/xDESGWWE8CqGf25sdgxiNABzSDGSEG248362K5ArKFXgrTt0tXvQsUZqmOYRVwiITgySG97097SGSGoGsJbDMPZH4kRnHS6wqjyQ6qQ/eB7G4WTNBCSLtRadiBadg086SG06agawerg96089578olGYqrmy/kB/1JdS+TPkGr1vdabwwAVo7SHSEGSEF086086985sfxy+upnalERAQi2aF2STap2Bj9hoGPjsesegsegsegId/gzlDyS8lsYSEGSEG0869859D0XnlcQeBow3dvTlbvBWAsDO2QMVR+UcHD8hrroRSEjSGSEG89697587445609SGSEEEGGSGEqxMJByiAjI9JED9rl/lDWGeIJuPYl==
-----END CERTIFICATE-----
    ```

2. **Add certificate**: From your [IBM Cloud Resource Dashboard ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){:new_window} IBM Blockchain network,
select the **Members** tab. Select **Add Certificate**, and paste the text string
(blob) from Step 1 into the **Certificate** field. Also specify a **Name**, and click
**Submit** to add the certificate to your member organization profile.

3. **Restart peers**: Remain on your IBM Cloud Resource Dashboard, and click **Restart** to restart your peers and refresh their copies of the Network Administrator Certificate. If you **Cancel** the restart, you will have to restart your peers manually before completing the authorization process.

4. **Sync certificate**: Sync the Network Administrator Certificate on all of your channel peers;
select the appropriate channel (or channels), and from the **Actions** menu, select **Sync Certificate**.

5. **Complete authorization**: Click **Done authorizing** to complete the service authorization process.

## What's next?
Proceed to the final service provisioning step: [Install and instantiate the service](install-instantiate-service.html).
