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

# Install and instantiate service chaincode
Once your organization Network Administrator has configured and authorized the
Blockchain Document Store service, network tools will **automatically** install
and instantiate the service chaincode on your channel peers.

**Authority/Role**: Blockchain Network Service Provider (automated)

For any blockchain network channel using the Blockchain Document Store service,
**ALL** organizations on the channel must have the service chaincode configured,
authorized, and installed on their peers. The service chaincode is instantiated (run)
only once on the channel, by any channel member. If necessary, a new channel can
be created for the purpose of using Blockchain Document Store.

## Install service chaincode procedure
Following successful service authorization, network tools take over the
service provisioning process and automatically install the service
chaincode on each member peer.

Each instance of the Blockchain Document Store service can be provisioned on only
one channel, per organization. For your organization to use Blockchain Document
Store on multiple network channels, the service must be purchased and provisioned
separately for each channel. However, you only need to [Register](register-entities.html){:new_window} once, and add the Network Administrator Certificate to the network once, for all of your organization channels.

## Instantiate service procedure
Following successful installation of the service on your channel peers, network
tools will automatically instantiate (run) the service on the channel. Instantiation does
not have to be repeated as additional organizations join the channel and install the service.

## What's next?
Manage your documents, as described in [Manage documents](manage-documents.html).
