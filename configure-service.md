---

copyright:
  years: 2019
lastupdated: "2019-02-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configure the service

Once your organization has subscribed to an **IBM Blockchain Platform** plan and created an instance of the **Blockchain Document Store** service, you must connect the service to your network. This connection creates a linkage to another member organization on the network that enables document sharing.

Complete the following steps to configure your organization's instance of the Blockchain Document Store service on your network channel peers:

1. **Copy blockchain network credentials JSON** (required):  
For **IBM Blockchain Platform** networks, Log in to your [IBM Cloud Services dashboard ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){:new_window}, and select your network instance. From the **Manage** tab click "Enter Monitor". Then from your network **APIs** tab, copy the **Network Credentials** JSON.

2. **Paste Network Credentials** (required):  
From your IBM Cloud Services dashboard, select your Blockchain Document Store instance. Select the **Network** tab and completed the required fields, including pasting your **Network Credentials** JSON from Step 1. Click the **Connect** button.

3. Add network administrators by IBM ID or IBM Cloud IAM Service ID.

4. Click **Connect**. Network tools will configure the service in a few minutes.

5. **Restart Network Peers** (required):
Restart your network peer nodes. Note that restarting nodes can lead to loss of processing transactions. Click **Yes** to confirm the node restart. This step is required for your blockchain network peers to recognize the new Blockchain Document Store service instance. Once your service instance is **connected** to your blockchain network, you will specify the specific network channels to connect the service to.

6. **Install and instantiate chaincode on your network channels**
Once you have configured the **Blockchain Document Store** service on your network, the service chaincode can be added to your network channels. To install and instantiate the service chaincode on a channel, click **Connect**. The connection status is shown and a confirmation message is displayed once the connection is complete.

## What's next?
[Connect an application to the service](blockchain-document-store/register-app.html) or [connect a solution to the service](blockchain-document-store/register-solution.html).
