---

copyright:
  years: 2018
lastupdated: "2018-04-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started
In this getting started tutorial, you will get set up to use **Blockchain
Document Store** to manage (upload, download, view, verify and share)
documents (Files and JSON), on an IBM Blockchain Platform network hosted on IBM Cloud.
The prerequisite steps to add your organization and users to an IBM Blockchain Solution,
using **Blockchain Solution Manager**, are also included.

## Before you begin
To get started using the **Blockchain Document Store** service, you will need
both an [IBMid ![External link icon](images/launch-glyph.svg "External link icon")](https://www.ibm.com/account/us-en/signup/register.html){:new_window} and an
[IBM Cloud account ![External link icon](images/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/registration/){:new_window}, which enable you to initiate or join an **IBM Blockchain Platform network on IBM Cloud**. To join an
existing network, you will need the **Network Initiator** to grant you administrator
access for your member organization. If you are the Network Initiator for a new network,
you will automatically be granted administrator access. In either case, your
organization must also purchase an IBM Blockchain Platform plan, and one instance
of Blockchain Document Store per channel.

To get started using Blockchain Document Store, complete the following prerequisites:

	{:pre}

1. Register, or log in, to the IBM network with your [IBMid ![External link icon](images/launch-glyph.svg "External link icon")](https://www.ibm.com/account/us-en/signup/register.html){:new_window}.
2. Register, or log in to [IBM Cloud ![External link icon](images/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/registration/){:new_window}.
3. Purchase an [IBM Blockchain Platform service plan ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/catalog/services/blockchain){:new_window}.
4. Set up governance for your IBM Blockchain Platform network (if necessary) by
completing steps 1-3, at [Govern the network ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/services/blockchain/get_start.html#getting-started-with-blockchain){:new_window}.
5. Define a channel to install and instantiate Blockchain Document Store on (if necessary), as described in steps 1-4, at [Configuring network resources and environment ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/services/blockchain/get_start.html#configuring-network-resources-and-environment){:new_window}.
6. Each member organization on the channel must purchase an instance of the Blockchain Document Store service,
which requires a network **connection profile** (JSON) and the network channel name. To obtain this information,
open the **Service Credentials** JSON file from your [IBM Cloud Resource Dashboard ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){:new_window}.
7. Purchase an instance of [Blockchain Document Store ![External link icon](images/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/catalog/services/blockchain-document-store){:new_window}.
When purchasing Blockchain Document Store, you must provide a list of administrators (email addresses) who
are authorized to onboard your organization and users.

## Step 1: Provision the service
Once your organization has purchased the Blockchain Document Store service, and has
joined or initiated an IBM Blockchain Platform network, your organization **Network
Administrator** will provision the service to your channel peers. Each organization must
provision one unique instance of Blockchain Document Store for each network **channel** that it joins.

Provision Blockchain Document Store as follows:
1. Start with the procedure to [configure the service](configure-service.html)
2. Following configuration, [authorize the service](authorize-service.html)
3. Network tools will then automatically [install and instantiate the service](install-instantiate-service.html).

## Step 2: Consume the service - Manage users
Once your organization Network Administrator has provisioned the Blockchain
Document Store service to your network channel peers, your **Organization Administrator**
will register your organization human and system users (including applications) to consume
the service. Follow the procedure described in [manage users](manage-users.html).

## Step 3: Consume the service - Manage documents
Once your instance of the Blockchain Document Store service is successfully
provisioned, and your organization and users are registered, your authenticated
users can start using the service to [manage documents](manage-documents.html).

## What's next?
Start provisioning the service, as described in [Configure the service](configure-service.html).
