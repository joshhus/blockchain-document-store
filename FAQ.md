---

copyright:
  years: 2018
lastupdated: "2018-04-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# FAQ

Before contacting Blockchain Document Store support, you can search the
FAQs below. You can also review the [Troubleshooting](troubleshooting.md)
information, which includes error messages and corrective actions.

FAQs: [APIs](APIs) | [Tokens](Tokens) |

----------

## APIs

**Q:** What **APIs** are available for me to interact with the service and network?

**A:** To initiate, join or manage an IBM Blockchain Solution on IBM Cloud (various levels of
administrator access required):
[Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window}.

**A:** To manage documents with Blockchain Document Store:
[Blockchain Document Store API ![External link icon](images/launch-glyph.svg "External link icon")](https://stage.pbsa-dev1.us-south.containers.mybluemix.net/docstore/swagger-ui.html.){:new_window}.

----------

## Tokens

**Q:** How do I exchange a Cloud IAM token for a service Onboarding token?

**A:** 

----------

**Users**: How do I add a new user to an instance of Blockchain Document Store?

**Add a human user**: Log in, with **Organization Administrator** access, to the
applicable solution<!-- and channel -->. Then initiate a PUT call to the **/v1/organizations/{organizationId}/users** endpoint,
at https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Users.

**Add a system user**: Log in, with **Organization Administrator** access, to the
applicable solution and channel. Then initiate a PUT call to the **/v1/organizations/{organizationId}/systems** endpoint,
at https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Systems/put_v1_organizations__organizationId__systems.

----------

How do I assign a role to a user?

**Human user**: Log in, with **Organization Administrator** access, to the
applicable solution and channel. Then initiate a PUT call to the **/v1/organizations/{organizationId}/users** endpoint;
at https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Users.
In the payload, specify one or more defined [roles](glossary.html#roles).

**System user**: Log in, with **Organization Administrator** access, to the
applicable solution and channel. Then initiate a PUT call to the **/v1/organizations/{organizationId}/systems** endpoint;
at https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Users.
in the payload, specify one or more defined [roles](glossary.html#roles).

----------

**Terminology**: How are blockchain and networking terms used in this environment?

Please see the [Glossary](glossary.html){:new_window} for Blockchain Document Store service terms and
definitions, including applicable [IBM Blockchain Platform ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/services/blockchain/index.html#ibm-blockchain-platform){:new_window} terms.

----------

**Purchase Service**: How do I purchase the Blockchain Document Store service?

Purchase the service through the [IBM Cloud Catalog ![External link icon](images/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/catalog/services/blockchain-document-store){:new_window}.

----------

**Roles**: How do I view role information for my network and users?

Use the **Admin** and **Roles** endpoints at [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window}.

----------
