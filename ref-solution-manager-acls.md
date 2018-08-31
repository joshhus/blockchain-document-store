---

copyright:
  years: 2018
lastupdated: "2018-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Blockchain Solution Manager API ACLs
The **Blockchain Solution Manager** API ACLs (Table 1.) describe the role assignments
required to call each API. Calls are made by an authenticated user (human,
system or application) submitting a request to a [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Developer/){:new_window} endpoint.

## ACLs by role

Table 1 below lists the defined ACL roles that are authorized to call each
Blockchain Solution Manager API:

   **Table 1. Blockchain Solution Manager API Access Control (ACLs)**

| METHOD /path                                             | Authorized ACL Roles         |
| -------------------------------------------------------- | ----------------- |
| **Admin**                                                |                   |
| GET /v1/administrators                                   | NetworkAdmin      |
| POST /v1/administrators                                  | NetworkAdmin      |
| DELETE /v1/administrators                                | NetworkAdmin      |
| PUT /v1/idp                                              | NetworkAdmin      |
| GET /v1/idp                                              | NetworkAdmin      |
| GET /v1/idp/{name}                                       | NetworkAdmin      |
| DELETE /v1/idp/{name}                                    | NetworkAdmin      |
|                                                          |                   |
| **Blockchain**                                           |                   |
| PUT /v1/networks                                         | NetworkAdmin,     |
|                                                          | servicebroker     |
| GET /v1/networks                                         | NetworkAdmin      |
| GET /v1/networks/{networkId}                             | NetworkAdmin      |
| GET /v1/networks/credentials/channels                    | NetworkAdmin,     |
|                                                          | BlockchainClient  |
| GET /v1/networks/certificates/admin_public_certificates  | NetworkAdmin,     |
|                                                          | servicebroker,    |
|						                                               | BlockchainClient  |
| GET /v1/networks/certificates/enrollment_certificates    | BlockchainClient  |
|                                                          |                   |
| **Solution**                                             |                   |
| PUT /v1/solutions                                        | NetworkAdmin,     |
|                                                          | SolutionAdmin     |
| GET /v1/solutions                                        | NetworkAdmin,     |
|                                                          | SolutionAdmin     |
|                                                          |                   |
| **Organizations**                                        |                   |
| PUT /v1/organizations                                    | NetworkAdmin,     |
|                                                          | SolutionAdmin     |
| GET /v1/organizations/{organizationId}                   | NetworkAdmin,     |
|                                                          | SolutionAdmin,    |
|							                                             | OrganizationAdmin |
| GET /v1/organizations/{organizationId}/roles             | NetworkAdmin,     |
|                                                          | SolutionAdmin,    |
|							                                             | OrganizationAdmin |
| GET /v1/organizations/{organizationId}/administrators    | NetworkAdmin,     |
|                                                          | SolutionAdmin,    |
|							                                             | OrganizationAdmin |
| POST /v1/organizations/{organizationId}/administrators   | NetworkAdmin,     |
|                                                          | SolutionAdmin,    |
|							                                             | OrganizationAdmin |
| DELETE /v1/organizations/{organizationId}/administrators | NetworkAdmin,     |
|                                                          | SolutionAdmin,    |
|							                                             | OrganizationAdmin |
|                                                          |                   |
| **Roles**                                                |                   |
| PUT /v1/roles                                            | NetworkAdmin,     |
|                                                          | SolutionAdmin     |
| PUT /v1/roles/{roleId}                                   | NetworkAdmin,     |
|                                                          | SolutionAdmin     |
| GET /v1/roles                                            | NetworkAdmin,     |
|                                                          | SolutionAdmin,    |
|							                                             | OrganizationAdmin |
| GET /v1/roles/{roleId}                                   | NetworkAdmin,     |
|                                                          | SolutionAdmin,    |
|							                                             | OrganizationAdmin |
| DELETE /v1/roles/{roleId}                                | NetworkAdmin,     |
|                                                          | SolutionAdmin     |
|                                                          |                   |
| **Organization Types**                                   |                   |
| PUT /v1/organization_types:                              | NetworkAdmin,     |
|                                                          | SolutionAdmin     |
| DELETE /v1/organization_types/{organizationTypeId}       | NetworkAdmin,     |
|                                                          | SolutionAdmin     |
| GET /v1/organization_types                               | NetworkAdmin,     |
|                                                          | SolutionAdmin,    |
|							                                             | OrganizationAdmin |
| GET /v1/organization_types/{organizationTypeId}          | NetworkAdmin,     |
|     Usage Note: SolutionAdmin and OrganizationAdmin      | SolutionAdmin,    |
|     (and User) roles can only search within their own    | OrganizationAdmin |
|     solutions.                                           |                   |
|	                                                         |                   |
| **Search**                                               |                   |
| GET /v1/search/systems                                   | NetworkAdmin,     |
|     Usage Note: OrganizationAdmin role can only search   | SolutionAdmin,    |
|     within their own solution and organization.          | OrganizationAdmin |
| GET /v1/search/users                                     | NetworkAdmin,     |
|     Usage Note: With the exception of the NetworkAdmin   | SolutionAdmin,    |
|     role, all users can only search within their own     | OrganizationAdmin,|
|     solutions.                                           | User,             |
|							                                             | SystemUser,       |
|							                                             | BlockchainClient, |
|							                                             | servicebroker     |
| GET /v1/search/organizations                             | NetworkAdmin,     |
|     Usage Note: Any authenticated user registered with   | SolutionAdmin,    |
|     the solution can invoke this API.                    | OrganizationAdmin,|
|                                                          | User,             |
|							                                             | SystemUser,       |
|							                                             | BlockchainClient, |
|							                                             | servicebroker     |
|                                                          |                   |
| **Users**                                                |                   |
| PUT /v1/organizations/{organizationId}/users             | OrganizationAdmin |
| DELETE /v1/organizations/{organizationId}/users/         |                   |
|        {userDocId}                                       | OrganizationAdmin |
| POST /v1/organizations/{organizationId}/users/           |                   |
|      {userDocId}/roles/{roleId}                          | OrganizationAdmin |
| DELETE /v1/organizations/{organizationId}/systems/       |                   |
|        {systemDocId}/roles/{roleId}                      | OrganizationAdmin |
|	                                                         |                   |
| **Systems**                                              |                   |
| PUT /v1/organizations/{organizationId}/systems           | OrganizationAdmin |
| DELETE /v1/organizations/{organizationId}/systems/       |                   |
|        {systemDocId}                                     | OrganizationAdmin |
| POST /v1/organizations/{organizationId}/systems/         |                   |
|      {systemDocId}/roles/{roleId}                        | OrganizationAdmin |
| DELETE /v1/organizations/{organizationId}/systems/       |                   |
|        {systemDocId}/roles/{roleId}                      | OrganizationAdmin |
|                                                          |                   |
| **OAuth**                                                |                   |
| GET /v1/jwks                                             | None              |   
|     Usage Note: Public key required.                     |                   |
| POST /v1/jwks                                            | None              |
|      Usage Note: Public key required.                    |                   |
| GET /v1/onboarding_jwks                                  | None              |
|     Usage Note: Public key required.                     |                   |
| POST /v1/auth/reference_token                            | SystemUser        |
|      Usage Note: Returns a reference token for the       |                   |
|      solution manager token specified in the body.       |                   |
| GET /v1/auth/introspect                                  | SystemUser        |
| POST /v0/token                                           | None              |
|      Usage Note: @deprecated. A system user requesting a |                   |
|      solution manager token by providing their service   |                   |
|      ID and apiKey (as password) can use this API. Refer |                   |
|      to /v1/iam/exchange_token.                          |                   |
| GET /v1/logins                                           | None              |
|     Usage Note: Starting point for human user            |                   |
|     authentication to receive a solution manager token.  |                   |
| POST /v1/iam/exchange_token                              | None              |
| POST /v1/iam/exchange_token/solution/                    |                   |
|      {solutionId}/organization/{organizationId}          | None              |
|                                                          |                   |
| POST /v1/iam/exchange_token/apps/{appId}                 | None              | |                                                          |                   |
| **Apps**                                                 |                   |
| PUT /v1/apps                                             | NetworkAdmin,     |
|                                                          | servicebroker     |
| DELETE /v1/apps/{appId}                                  | NetworkAdmin,     |
|                                                          | servicebroker     |
| GET /v1/apps                                             | NetworkAdmin,     |
|                                                          | servicebroker,    |
|						                                               | Application       |
| GET /v1/apps/{appId}                                     | NetworkAdmin,     |
|                                                          | servicebroker,    |
|							                                             | Application       |
| PUT /v1/apps/{appId}/policy                              | NetworkAdmin,     |
|                                                          | servicebroker,    |
|						                                               | Application       |
| GET /v1/apps/{appId}/policy                              | NetworkAdmin,     |
|     Usage Note: Application user appId that matches      | servicebroker,    |
|     the path appId parameter.                            | Application,      |
| GET /v1/apps/{appId}/chaincodes                          | NetworkAdmin,     |
|     Usage Note: Not yet implemented                      | OrganizationAdmin |
| PUT /v1/apps/{appId}/chaincodes                          | NetworkAdmin,     |
|     Usage Note: Not yet implemented                      | OrganizationAdmin |
|						                                               |                   |
| **Developer**                                            |                   |
| GET /api-docs.json                                       | None              |
|                                                          |                   |
{: caption="Table 1. Blockchain Solution Manager API Access Control (ACLs)" caption-side="top"}
