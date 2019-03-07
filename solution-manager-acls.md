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
that are authorized to call each endpoint. Calls are made by an authenticated and
authorized user (human, system or application) submitting a request to the
Blockchain Solution Manager API.

## ACLs by role
Table 1 below lists the defined ACL roles that are authorized to call each
Blockchain Solution Manager API endpoint. To access restricted endpoints, users
must **Authorize** by clicking on a lock icon in the API. (Endpoints with no lock
icon can be called by any registered user.)

   **Table 1. Blockchain Solution Manager API Access Control (ACLs)**

| <br>METHOD /path                                             | Authorized <br>ACL Roles         |
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
| PUT /v1/networks                                         | NetworkAdmin, servicebroker  |
| GET /v1/networks/{networkId}                             | NetworkAdmin      |
| GET /v1/networks/certificates/admin_public_certificates  | NetworkAdmin, servicebroker, BlockchainClient  |
| GET /v1/networks/certificates/enrollment_certificates    | BlockchainClient  |
| GET /v1/networks/credentials/channels                    | NetworkAdmin, BlockchainClient  |
|                                                          |                   |
| **Solution**                                             |                   |
| PUT /v1/solutions                                        | NetworkAdmin, SolutionAdmin  |
| GET /v1/solutions                                        | NetworkAdmin, SolutionAdmin  |
|                                                          |                   |
| **Organizations**                                        |                   |
| PUT /v1/organizations                                    | NetworkAdmin, SolutionAdmin  |
| GET /v1/organizations/{organizationId}                   | NetworkAdmin, SolutionAdmin, OrganizationAdmin  |
| GET /v1/organizations/{organizationId}/administrators    | NetworkAdmin, SolutionAdmin, OrganizationAdmin |
| POST /v1/organizations/{organizationId}/administrators   | NetworkAdmin, SolutionAdmin, OrganizationAdmin |
| DELETE /v1/organizations/{organizationId}/administrators | NetworkAdmin, SolutionAdmin, OrganizationAdmin |
|                                                          |                   |
| **Roles**                                                |                   |
| PUT /v1/roles                                            | NetworkAdmin, SolutionAdmin  |
| GET /v1/roles                                            | NetworkAdmin, SolutionAdmin, OrganizationAdmin |
| PUT /v1/roles/{roleId}                                   | NetworkAdmin, SolutionAdmin  |
| DELETE /v1/roles/{roleId}                                | NetworkAdmin, SolutionAdmin  |
| GET /v1/roles/{roleId}                                   | NetworkAdmin, SolutionAdmin, OrganizationAdmin |
|                                                          |                   |
| **Organization Types**                                   |                   |
| PUT /v1/organization_types:                              | NetworkAdmin, SolutionAdmin  |
| DELETE /v1/organization_types/{organizationTypeId}       | NetworkAdmin, SolutionAdmin  |
| GET /v1/organization_types                               | NetworkAdmin, SolutionAdmin, OrganizationAdmin |
| GET /v1/organization_types/{organizationTypeId}  <br>   Usage Note: SolutionAdmin and OrganizationAdmin  (and User) roles can only search within their own solutions  | NetworkAdmin, SolutionAdmin, OrganizationAdmin |
|	                                                         |                   |
| **Search**                                               |                   |
| GET /v1/search/systems  <br>   Usage Note: OrganizationAdmin role can only search within their own solution and organization. | NetworkAdmin, SolutionAdmin, OrganizationAdmin |
| GET /v1/search/users  <br>   Usage Note: With the exception of the NetworkAdmin role, all users can only search within their own solutions. | NetworkAdmin, SolutionAdmin, OrganizationAdmin, User, SystemUser, BlockchainClient, servicebroker  |
| GET /v1/search/organizations  <br>   Usage Note: Any authenticated user registered with the solution can call this endpoint. | NetworkAdmin, SolutionAdmin, OrganizationAdmin, User, SystemUser, BlockchainClient, servicebroker  |
|                                                          |                   |
| **Users**                                                |                   |
| PUT /v1/organizations/{organizationId}/users             | OrganizationAdmin |
| DELETE /v1/organizations/{organizationId}/users/userDocId}  | OrganizationAdmin |
| POST /v1/organizations/{organizationId}/users/{userDocId}/roles/{roleId} | OrganizationAdmin |
| DELETE /v1/organizations/{organizationId}/systems/{systemDocId}/roles/{roleId} | OrganizationAdmin |
|	                                                         |                   |
| **Systems**                                              |                   |
| PUT /v1/organizations/{organizationId}/systems           | OrganizationAdmin |
| DELETE /v1/organizations/{organizationId}/systems/{systemDocId}  | OrganizationAdmin |
| POST /v1/organizations/{organizationId}/systems/{systemDocId}/roles/{roleId} | OrganizationAdmin |
| DELETE /v1/organizations/{organizationId}/systems/{systemDocId}/roles/{roleId} | OrganizationAdmin |
|                                                          |                   |
| **OAuth**                                                |                   |
| GET /v1/jwks <br> Usage Note: Public key required.      | No restrictions              |  
| POST /v1/jwks  <br>  Usage Note: Public key required.   | No restrictions              |
| GET /v1/onboarding_jwks  <br>   Usage Note: Public key required.  | No restrictions      |
| POST /v1/auth/reference_token  <br>   Usage Note: Returns a reference token for the solution manager token specified in the body. | SystemUser |
| GET /v1/auth/introspect                                 | SystemUser        |
| GET /v1/logins  <br>   Usage Note: Starting point for human user authentication to receive a solution manager token.  | No restrictions  |
| POST /v1/iam/exchange_token/solution/{solutionId}/organization/{organizationId} | No restrictions  |
| POST /v1/iam/exchange_token/apps/{appId}                 | No restrictions              |
| GET /v1/lgoout                                           | No restrictions              |
|                                                          |                   |
| **Applications**                                         |                   |
| PUT /v1/apps                                             | NetworkAdmin, servicebroker     |
| DELETE /v1/apps/{appId}                                  | NetworkAdmin, servicebroker     |
| GET /v1/apps                                             | NetworkAdmin, servicebroker, Application   |
| GET /v1/apps/{appId}                                     | NetworkAdmin, servicebroker, Application   |
| PUT /v1/apps/{appId}/policy                              | NetworkAdmin, servicebroker, Application   |
| GET /v1/apps/{appId}/policy <br>   Usage Note: Application user appId that matches the appId parameter. | NetworkAdmin, servicebroker, Application |
| GET /v1/apps/{appId}/chaincodes                          | NetworkAdmin, OrganizationAdmin    |
| PUT /v1/apps/{appId}/chaincodes                          | NetworkAdmin, OrganizationAdmin    |
|						                                               |                   |
| **Developer**                                            |                   |
| GET /api-docs.json                                       | No restrictions              |
|                                                          |                   |
{: caption="Table 1. Blockchain Solution Manager API Access Control (ACLs)" caption-side="top"}
