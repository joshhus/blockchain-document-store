---

copyright:
  years: 2018
lastupdated: "2018-05-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Manage users
Once your organization **Network Administrator** has provisioned an instance of the
Blockchain Document Store service to your network channel peers, you will register users
with the solution. A **Solution Administrator** for your organization will register your
**human users** and **system users** (including **applications**) by authenticating their
identities to Blockchain Solution Manager. Once authenticated, all users are
authorized to interact with the service, within the limits of their assigned network roles.

**Authority/Role**: Organization Solution Administrator  
**Related documentation**: [Blockchain Solution Manager API overview](solution-manager-api.html)  
**Swagger interface**: [Blockchain Solution Manager API](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/)

## Blockchain Solution Manager
[Blockchain Solution Manager](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/) provides multiple functions for IBM Blockchain networks, following the [OAuth 2.0 ![External link icon](images/launch-glyph.svg "External link icon")](https://oauth.net/2/){:new_window} specification:
- Registers organizations, users (human and system) and applications
- Manages IBM Blockchain enrollment certificates for registered users
- Supports configuration of OpenID-compliant identity providers
- Allows Cloud IAM-based system user authentication.

## User registration
The initial registration of human users, system users and applications with an
IBM Blockchain Solution (for Blockchain Document Store, the solution is created by default),
is done by a **Solution Administrator** for a registered Organization:
1. An organization Solution Administrator authenticates to [Blockchain Solution Manager](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/)
2. Using the Blockchain Solution Manager API, a Solution Administrator adds their organization
users by specifying the User IDs (human users) and Service IDs (System Users and Applications)
that are registered with their identity service provider.
3. Upon user login, the identity service provider redirects to Blockchain Solution Manager to obtain an **Onboarding Token**.
4. The **Onboarding Token** returned by Blockchain Solution Manager is valid, for a limited time,
as proof of identity for the user to interact with the Blockchain Document Store service. (Note that **System Users"
must first exchange their **Onboarding Token** for a **Reference Token.**

### Creating Service IDs
Registering **System Users** with the Blockchain Document Store service requires an organization
**Solution Administrator** to create a unique IBM Cloud Service ID for each system user (including applications):
1. Log in (as Solution Administrator) to your [IBM Cloud Resource Dashboard ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){:new_window}.
2. Click on **Manage** in the top-right menu bar.
3. Select the **Security > Identity and Access** option.
4. The **Users** page for the account will load by default; click on the **Service IDs** tab
in the left pane.
5. Click **Create +** to create a new Service ID. You must record the value of the Service ID (e.g. ServiceId-3bf785-449c-422-afd9-12db3913b).
6. On the **Manage Service ID** page, click **API keys**.
7. Click **Create +** to create an API key (i.e. password) for the Service ID. Enter a
**Name** and a **Description**, and click **Create**. You must save the API key, in a secure location.
8. Configure each registered system user (and application) to obtain an **Onboarding Token** by calling the /v1/iam/exchange_token/solution/{solutionId}/organization/{organizationId} endpoint (or for applications, the **/v1/iam/exchange_token/apps/{appId}** endpoint).

## General authentication Flow
To authenticate human users, system users and applications, the Blockchain Solution Manager
API interacts with the user's identity service, via JSON Web Tokens:
1. The user authenticates their identity, using either IBMid or their third-party
identity service.
2. The user receives a JSON Web Token (JWT) from Blockchain Solution Manager.
3. The user passes their JWT to the Blockchain Document Store service, as proof of identity.
4. Blockchain Document Store verifies the JWT, using the public key from Blockchain Solution Manager.
5. If the token has not been altered since its creation, verification is successful.

Continue reading below for the specific authentication steps for each user type:

### Human user authentication (UI-based)
Blockchain Solution Manager authenticates human users through the following interactions. Through a UI,
human users select their identity provider, authenticate, and receive an **Onboarding Token**, as follows:
1. The human user connects to the service onboarding URL for their organization, *service-onboarding-basepath*/onboarding/v1/logins, and selects their identity service provider. **Note**: The *service-onboarding-basepath* is unique per organization; see your
blockchain network service provider.
2. The human user is redirected to the login page for their identity service
provider, where the user submits their credentials (email address and password).
4. The identity provider returns a JSON Web Token (JWT) for the user to Blockchain Solution Manager.
5. A new access token is generated by Blockchain Solution Manager and
returned to the user at the URL for their organization: *service-onboarding-basepath*/onboarding/v1/logins.
6. The human user passes this **Onboarding Token**, as proof of identity, to the Blockchain
Document Store service.
7. Blockchain Document Store verifies the **Onboarding Token** by using the public key
from Blockchain Solution Manager.
8. If the **Onboarding Token** has not been altered since it was initially signed,
verification of the user identity is successful, and the human user can proceed to using the
Blockchain Document Store service.

### System user authentication (programmatic)
Blockchain Solution Manager authenticates system users (with the exception of applications)
through the following interactions. System users authenticate through
the [IBM Cloud IAM endpoint ![External link icon](images/launch-glyph.svg "External link icon")](https://iam.ng.bluemix.net/oidc/token,){:new_window},
and then exchange their **IAM Token** for a service **Onboarding Token**, as follows:
1. A **Solution Administrator** for the organization creates a Service ID for the
system user, as described previously in [Creating Service IDs](#creating-service-ids).
2. The system user authenticates through the IBM Cloud IAM endpoint
and requests an **IAM Token** by API key:
    ```
    curl -v -u "demo:demo" -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=$USER_API_KEY" "https://iam.ng.bluemix.net/oidc/token"   > iam.apikey.token
    ```
3. The system user specifies the received **IAM Token** in the **Authorization Header** of a
request for an **Onboarding Token**, which is passed to Blockchain Solution Manager for
verification and decoding into human-readable strings:

    ```
    curl -k  -H "Content-Type: application/json" --data-binary @iam.apikey.token -X POST "/v1/iam/exchange_token/solution/{solutionId}/organization/{organizationId}"
    ```
4. If verified, the system user receives an **Onboarding Token** from Blockchain Solution Manager.
5. Blockchain Document Store verifies the **Onboarding Token** by using the public key
from Blockchain Solution Manager.
6. If the **Onboarding Token** has not been altered since it was initially signed,
verification of the identity is successful and the system user can proceed to using the
service.

### Application authentication (programmatic)
Blockchain Solution Manager authenticates applications only (not other system users) through
the following interactions. Applications authenticate through the [IBM Cloud IAM endpoint ![External link icon](images/launch-glyph.svg "External link icon")](https://iam.ng.bluemix.net/oidc/token,){:new_window}
and then exchange their **Cloud IAM Token** for a service **Onboarding Token**, as follows:
1. A Solution Administrator for the organization creates a Service ID (ServiceId) for the
application, as described previously in [Creating Service IDs](#creating-service-ids).
2. The application (ServiceId) authenticates through the IBM Cloud IAM endpoint
and requests a **Cloud IAM Token** by API key:
    ```
    curl -v -u "demo:demo" -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=$USER_API_KEY" "https://iam.ng.bluemix.net/oidc/token"   > iam.apikey.token
    ```
3. The application adds the received **IAM Token** to the authorization header of a
request for an **Onboarding Token**, which it passes to Blockchain Solution Manager for
verification and decoding into human-readable strings:
    ```
    curl -k  -H "Content-Type: application/json" --data-binary @iam.apikey.token -X POST "/v1/iam/exchange_token/apps/{appId}"
    ```
4. If verified, the application receives an **Onboarding Token** from Blockchain Solution Manager.
5. Blockchain Document Store verifies the **Onboarding Token** by using the public key
of Blockchain Solution Manager.
6. If the **Onboarding Token** has not been altered since it was initially signed,
verification of the identity is successful and the application can proceed to using the
service. **Note**: The Environment Variable **DREF_TOKEN_MAX_TIMEOUT**=3h can be used to
override the default **Reference Token** timeout of 3 hours.

Applications can submit an **Onboarding Token** on behalf of another user. In
this case, the application receives a **Reference Token**, which has a longer TTLs
(time to live) than an **Onboarding Token**. All **Reference Tokens** are intended for
applications to use when performing long-running transactions on behalf of a user. Only applications can use the
**Reference Token** endpoint. **Note:** The Environment Variable **JWT_TOKEN_EXPIRES_IS**=3h
can be used to override the default **Onboarding Token** expiration time of 3 hours.

Applications can include a policy definition, via the  [/v1/apps/{appId}/policy](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/) endpoint, to grant access to users, roles, organizations and other applications. Any application accessing Blockchain Solution Manager must include the  **SM_SOLUTION_READER** static variable.

## Blockchain Solution Manager API
The Blockchain Solution Manager API allows authorized users to register their
organization users, system users and applications with an IBM Blockchain solution:

### Public key endpoint
The public key endpoint *service-onboarding-basepath*/v1/onboarding_jwks provides the public key
that signs tokens. This public key is used by applications to verify tokens received from Blockchain Solution Manager. **Note**: The *service-onboarding-basepath* is unique per organization; see your blockchain network service provider.

### Introspect endpoint
The introspect endpoint  [OAuth /v1/auth/introspect ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window} returns human-readable output in **Reference Token** format.

### JSON Web Tokens (JWTs)
Blockchain Solution Manager uses **JSON Web Tokens** (JWTs) to verify the identities of human users, system users and applications. JWTs enable the secure passing of data between authenticated users, for a set length of time. The JWT format is a period-delimited triple of base64-encoded data that identifies the organization, user and solution. For more details, see [JSON Web Tokens ![External link icon](images/launch-glyph.svg "External link icon")](https://jwt.io/introduction/){:new_window}.

## What's next?
Proceed to [Manage documents](manage-documents.html).
