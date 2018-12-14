---

copyright:
  years: 2018
lastupdated: "2018-12-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Install and instantiate chaincode

Once you have configured and authorized the **Blockchain Document Store** service for your organization, the **service chaincode is automatically installed and instantiated on your network channel peers**.

For any organization to use the Blockchain Document Store service, all organizations on the network channel must have the service chaincode configured, authorized, and installed on their peers. **The service chaincode is instantiated (run) only once on the channel, by any organization on the channel.** If necessary, a new channel can be created for the purpose of using Blockchain Document Store.

Each instance of the Blockchain Document Store service can be provisioned on only one channel, per organization. For your organization to use Blockchain Document Store on multiple network channels, the service must be purchased and provisioned separately for each channel. However, you only need to configure the service once, and add the Network Administrator Certificate to the network once, for all of your organization's channels.

## Install service chaincode
Following successful service authorization, network tools take over the service provisioning process and automatically install the service chaincode on each member peer.

## Instantiate service chaincode
Following successful installation of the service on your channel peers, network tools will automatically instantiate (run) the service on the channel. Instantiation does not have to be repeated as additional organizations join the channel and install the service.

## What's next?
Connect an application or connect a solution to the service.
