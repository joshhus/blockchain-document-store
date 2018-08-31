---

copyright:
  years: 2018
lastupdated: "2018-03-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configure the service
Once your organization has purchased an instance of the IBM Blockchain Document Store
service, and an IBM Blockchain Platform service plan, your **Network Administrator** will
provision the service to your network channel peers. The first step in
**provisioning** is to **configure** the Blockchain Document Store service.

**Authority/Role:** Member Organization [Network Administrator](glossary.html#network-administrator){:new_window}

To configure an instance of the IBM Blockchain Document Store
service on your channel peers, your Network Administrator connect to the IBM Cloud
Service Dashboard for your organization, at *service-onboarding-basepath*/onboarding.
**Note**: The *service-onboarding-basepath* is unique per organization; see your
blockchain network service provider.  

**Attention**: One unique instance of the Blockchain Document Store service is required per
member organization, per network channel.

## Configure service procedure
Complete the following steps to configure your organization's instance of the
Blockchain Document Store service on your channel peers:

1. **Copy network configuration JSON** (required):  
Log in to your [IBM Cloud Resource Dashboard ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){:new_window}, and select your
IBM Blockchain network. From the **Service Credentials** tab,
copy the blockchain network configuration JSON. The following example is a
snippet of the complete [network configuration JSON example](configure-json-example.html){:new_window}.

    ```
    {
	    "name": "network",
	    "x-networkId": "uuid-uuid1",
	    "x-type": "hlfv1",
	    "x-app-channel": "mychannel",
	    "description": "local network connection profile formatted into IBM Blockchain Platform format",
	    "version": "1.0.0",
	    "client": {
		    "organization": "org1"
	    },
	    "channels": {
		    "mychannel": {
			    "orderers": [
			    	"orderer.example.com"
			    ],
			    "peers": {
				    "peer0.org1.example.com": {
					    "endorsingPeer": true,
              "chaincodeQuery": true,
              "ledgerQuery": true,
              "eventSource": true
				    },
				    "peer0.org2.example.com": {
					    "endorsingPeer": true,
              "chaincodeQuery": true,
              "ledgerQuery": true,
              "eventSource": true
				    }
			    }
		    }
	    }

    ```

2. **Paste IBM Blockchain network JSON** (required):  
In the IBM Cloud Service Dashboard for your organization, at *service-onboarding-basepath*/onboarding, paste the JSON from Step 1 into the **Blockchain network configuration (JSON)** field.
**Note**: The *service-onboarding-basepath* is unique per organization; see your
blockchain network service provider.  

3. **Select channel** (required):  
In the IBM Cloud Service Dashboard for your organization (from Step 2), select the channel to configure the service on. The list of channels is populated by pasting the network JSON in Step 2.

4. **Enter Blockchain solution ID** (optional):  
Specify a unique Blockchain solution ID. **If** you enter a Blockchain solution ID,
the fields in the next two steps are presented.

5. **Enter Blockchain solution description** (optional):  
Specify a Blockchain solution description.

6. **Enter Blockchain Solution Manager URL** (optional):  
Specify the URL to your solution onboarding endpoint, at
*service-onboarding-basepath*/onboarding.

7. **Enter Blockchain organization ID** (optional):  
Specify a unique IBM Blockchain organization ID.

8. **Enter Blockchain organization description** (optional):  
Specify an IBM Blockchain organization description.

9. **Enter Administrator emails** (required):  
Specify your organization Network Administrator email addresses.

10. **Submit** (required):  
Click the **Submit** button to configure the service.

If you did not receive any error messages, the instance of the Blockchain Document
Store service is now configured on your specified IBM Blockchain network channel peers.

## What's next?
Proceed to the next service provisioning step: [Authorize the service](authorize-service.html).
