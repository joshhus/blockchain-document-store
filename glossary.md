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

# Glossary
This glossary provides terms and definitions for understanding IBM Blockchain
Solutions running on an instance of [IBM Blockchain Platform](https://console.bluemix.net/docs/services/blockchain/index.html){: new_window}
hosted on IBM Cloud.

Contents:  
- [IBM Blockchain Solution terms](#ibm-blockchain-solutions-terms)
- [IBM Blockchain Platform terms](#ibm-blockchain-platform-terms)
- [Blockchain Network and Security terms](#blockchain-network-and-security-terms)

## IBM Blockchain Solution terms

**Application** - An automated service, with a unique Service ID, that processes
data for a solution. Solution login for an Application is programmatic, using a
serviceid/apikey combination via IBM CloudIAM.

**System User** - An automated program, with a unique Service ID, that sends data
to or receives data from the solution. Solution login for a System User is programmatic,
using a serviceid/apikey combination via IBM CloudIAM.

**Human User** - A user, with a unique User ID, who interacts with the solution
via a UI. Solution login for a human user is via UI, using an email/password
combination via SSO.

**IBM Blockchain Network** - A secure, permissioned instance of IBM Blockchain
Platform running one or more IBM Blockchain Solutions.
IBM Blockchain Networks are hosted on IBM Cloud.

**IBM Blockchain Solution** - A collection of
applications and services that provide blockchain network functions
to member organizations.

**IBM Blockchain Solution Manager** - An array of functions for organizations
to manage their blockchain network, solution, services, organizations and users.

**IBM Blockchain Document Store** - SaaS that enables organizations
to join an IBM Blockchain network, onboard users and solutions, and store and manage
documents. IBM Blockchain Document Store is a blockchain network application that
consists of a file storage service, a blockchain ledger service, and a solution manager
component. Within the context of IBM Cloud, Blockchain Document Store as a whole
is referred to as a service (SaaS).

{: #organization-administrator}
**Organization Administrator** - An authenticated Organization Administrator
has the authority to manage their organization, and its human users and system
users (including applications). The Organization Administrator role is assigned to
each member organization, which can assign the role to one or more of its registered
human users.

<!--
{: #service-administrator}
**Service Administrator** - An authenticated Service Administrator has the
authority to manage solutions and service applications only, on behalf of their
organization. The Service Administrator role is assigned to each member
organization, which can assign the role to one or more of its registered human users.
TBA - replace with Network Administrator? -->

**Service Chaincode** - Source code for a service application, such as Blockchain
Document Store, which is installed and instantiated on channel peers.

{: #solution-administrator}
**Solution Administrator** - An authenticated Solution Administrator has the
authority to manage organization types, roles and organizations. The Solution
Administrator role is assigned to each member organization, which can assign the
role to one or more of its registered human users.

{: #roles}
**Roles** - Roles are predefined access controls (aka ACLs), which provide specific
access to Blockchain Document Store functions for authenticated, authorized
users. The following roles are predefined: `NetworkAdmin`, `SolutionAdmin`,
`OrganizationAdmin`, `User`, `SystemUser`, `BlockchainClient`, `servicebroker`
and `Application`.

**Onboarding Token** - Blockchain Solution Manager uses JSON Web Tokens (JWTs) to
verify the identities of human users, system users and applications. An **Onboarding
Token** enables the secure passing of data between authenticated users, for a set
length of time. The JWT format is a period-delimited triple of base64-encoded data
(i.e. unreadable by a human) that identifies the organization, user and solution.
For additional JWT reference information, see [JSON Web
Tokens ![External link icon](images/launch-glyph.svg "External link icon")](https://jwt.io/introduction/){:new_window}.

**Reference Token** - A human-readable access token that
is provided to a trusted application only. Each application must exchange its
**Onboarding Token** for a **Reference Token**, for inclusion in API calls.

**IAM Token** - System users, including applications, must first request an IBM Cloud **IAM Token**, which is then included with an **Onboarding Token** request.

## IBM Blockchain Platform terms
**IBM Blockchain Network** - A consortium, or collection of organizations,
that have joined the same instance of an IBM Blockchain Platform network. By
accepting the invitation to join, each organization has become a member of the
network, and implicitly consented to the governance policies set by the Network
Initiator.

**Network Initiator** - Any organization that purchases an IBM Blockchain Platform
plan on IBM Cloud is a Network Initiator. Purchasing a plan initiates an
IBM Blockchain network for the organization, by default. The Network Initiator
then sets the network governance policies, and invites other IBM Blockchain
organizations to join their network, i.e., to become a **Member**. Membership
in an IBM Blockchain Network is by invitation only, from the Network Initiator.

**Channel** - A group of blockchain network member organizations that
share a ledger and documents database, for the purpose of conducting
private and confidential transactions between channel peers.

## IBM Blockchain Network and Security terms

{: #bearertoken}
**Bearer token** - An HTTP authentication security token that
grants access to the bearer of the token. When the bearer of the token sends a
request to a network resource, they must include the bearer token in the
Authorization header of an API call: 'Authorization: Bearer &lt;token&gt;'.
For details, see [Swagger Bearer Authentication ![External link icon](images/launch-glyph.svg "External link icon")](https://swagger.io/docs/specification/authentication/bearer-authentication/){:new_window}.

{: #jwks}
**JWKS** - A JSON Web Key Set (JWKS) contains the public keys used to verify any
JSON Web Token (JWT) issued by the authorization server. For details, see
[JSON Web Key Set (JWKS) ![External link icon](images/launch-glyph.svg "External link
icon")](https://auth0.com/docs/jwks){:new_window}.

**OAuth 2.0** - OAuth 2.0 is the IBM Blockchain Solutions protocol for providing
application and service authentication and authorization to users, systems and
applications. Authentication for human users is a valid email address and
password combination; authentication for systems is a Service ID and API key
combination. For details, see
the [OAuth 2.0 ![External link icon](images/launch-glyph.svg "External link icon")](https://oauth.net/2/){:new_window} specification.

**Password Grant** - The password grant type is used when an application exchanges
a user’s username and password for an access token. For details see
[OAuth Password Grant ![External link icon](images/launch-glyph.svg "External link icon")](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/){:new_window}.
