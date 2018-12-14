---

copyright:
  years: 2018
lastupdated: "2018-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Manage users

Once you have a) connected your instance of the **Blockchain Document Store** service
to another IBM Blockchain Platform member organization, and b) configured access to
your service as either an application or an IBM Blockchain solution, you will register and manage your users.

First, you will register your **human users** and **system users** by authenticating
their identities to the **Blockchain Solution Manager** component of the service. As
described below, the registration process differs slightly for each user type&mdash;registering a **system
user** requires first obtaining a **Service ID** from IBM Cloud IAM.

## Blockchain Solution Manager

The **Blockchain Solution Manager** component of **Blockchain Document Store* is the interface to user management functions, following the [OAuth 2.0 ![External link icon](images/launch-glyph.svg "External link icon")](https://oauth.net/2/){:new_window} specification. Use the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/UI%20OAUTH%20Login%20Flow/get_v1_logins){:new_window} for all user management tasks:
- Register your organization and users (human and system)
- Manage IBM Blockchain Platform enrollment certificates for all users
- Support configuration of OpenID-compliant identity providers
- Allow IBM Cloud IAM-based system user authentication.

To complete these tasks, you need to acquire and manage authorization tokens for
your human and system users, as described below.

## Manage tokens

To register and manage your human and system users through the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window}, you will need to acquire and specify **Onboarding Tokens**, as applicable:

**Onboarding Token** - Service Onboarding Tokens are issued to both human and system users, by role. There are four distinct user roles, and any one user can be assigned to multiple roles in their Organization: **Network Administrator**, **Solution Administrator**, **System User**, **Human User**.

**IBM Cloud IAM Token**: - System users must (programmatically) first obtain an IBM Cloud IAM Token and then exchange it for a service Onboarding Token:

**Acquire Cloud IAM Token**: ! TBA ... curl ? //iam.ng.bluemix.net/oidc/token)

Exchange Cloud IAM System User Access Token:  Configure system users to call the following endpoint: ** *service-onboarding-basepath*/onboarding/v1/iam/exchange_token/solution/{solutionId}/organization/{organizationId} **

!! TBA - this is app token management - move it under that section of doc?

Exchange Cloud IAM Application Access Token:  ** *service-onboarding-basepath*/onboarding/v1/iam/exchange_token/solution/{solutionId}/organization/{organizationId} **



## Create User IDs

! TBA this is interesting, because the Cloud https://console.bluemix.net/iam/#/users
interface allows creating system IDs, but this appears to only allow "inviting"
users, by email address - so there is no created human user IDs step per se?

To register your **Human Users** with IBM Food Trust, you must create a unique **User ID** for each human user, as follows:

! TBA - what about creating their Organization? Don't they have to do that
first before user IDs. Or can they do that here with "organizationId" parameter?

1. Using the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Organization%20Users/put_v1_organizations__organizationId__users){:new_window}, you will execute a **PUT** call (details in Step 2) to the  ** *service-onboarding-basepath*/onboarding/v1/organizations/{organizationId}/users ** endpoint. **Attention**: The ** *service-onboarding-basepath* ** is unique per organization; see your blockchain network service provider.  

2. Create your new human user definitions in JSON, and paste them into the **Body** of the  **PUT** call to the ** /onboarding/v1/v1/organizations/{organizationId}/users** endpoint. Specifying your *organizationId* is required. For example:

    ```
    {
    "name": "string",
    "id": "string",
    "userId": "user1@ibm.com",
    "organizationId": "string",
    "solutionId": "string",
    "roles": [
      "A list of role Ids"
    ],
    "onboardedBy": "string"
  }
    ```


## Create System IDs

Before registering your **System Users**, you must create a unique
IBM Cloud **Service ID** for each system user, as follows:

TBA. hmmm, do we want this below, or instead the /v1/organizations endpoint?

1. Log in to your [IBM Cloud Resource Dashboard ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){:new_window}.
2. Click on your instance of the **Blockchain Document Store** service.
3. From the **TOP menu bar**, select the **Manage > Security > Identity and access** option.
4. The **Users** page for the account will load by default; click on the **Service IDs** tab
in the left pane.
5. Click the **Create +** button on the right to create a new Service ID; you **must record the value of the Service ID** (e.g. ServiceId-3bf785-449c-422-afd9-12db3913b).
6. On the **Manage Service ID** page, click the **API keys** tab.
7. Click the **Create +** button on the right to create an API key (i.e. password) for the Service ID. Enter a **Name** and a **Description**, and click **Create**. You **must save the API key manually** in a secure location. (TBA !! is this the IBM Cloud IAM token?)
8. Configure each registered system user to obtain a service **Onboarding Token** by calling the ** *service-onboarding-basepath*/v1/iam/exchange_token/solution/{solutionId}/organization/{organizationId} ** endpoint (or for applications, the **/v1/iam/exchange_token/apps/{appId}** endpoint).

## Human user authentication (UI-based)

Blockchain Solution Manager authenticates human users through the following interactions. Through a UI,
human users select their identity provider, authenticate, and receive an **Onboarding Token**, as follows:

1. The human user connects to the service onboarding URL for their organization, *service-onboarding-basepath*/onboarding/v1/logins, and selects their identity service provider. **Note**: The *service-onboarding-basepath* is unique per organization; see your
blockchain network service provider.

2. The human user is redirected to the login page for their identity service
provider, where the user submits their credentials (email address and password).

3. The identity provider returns a JSON Web Token (JWT) for the user to Blockchain Solution Manager.

4. A new access token is generated by Blockchain Solution Manager and
returned to the user at the URL for their organization: *service-onboarding-basepath*/onboarding/v1/logins.

5. The human user passes this **Onboarding Token**, as proof of identity, to the Blockchain
Document Store service.

6. Blockchain Document Store verifies the **Onboarding Token** by using the public key
from Blockchain Solution Manager.

7. If the **Onboarding Token** has not been altered since it was initially signed,
verification of the user identity is successful, and the human user can proceed to using the
Blockchain Document Store service.

## System user authentication (programmatic)

Blockchain Solution Manager authenticates system users (with the exception of applications)
through the following interactions. System users authenticate through
the [IBM Cloud IAM endpoint ![External link icon](images/launch-glyph.svg "External link icon")](https://iam.ng.bluemix.net/oidc/token,){:new_window},
and then exchange their **IBM Cloud IAM Token** for a service **Onboarding Token**, as follows:

1. A **Solution Administrator** for the organization creates a Service ID for the
system user, as described previously in [Creating Service IDs](#creating-service-ids).

2. The system user authenticates through the IBM Cloud IAM endpoint
and requests an **IBM Cloud IAM Token** by API key:
    ```
    curl -v -u "demo:demo" -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=$USER_API_KEY" "https://iam.ng.bluemix.net/oidc/token"   > iam.apikey.token
    ```
3. The system user specifies the received **IBM Cloud IAM Token** in the **Authorization Header** of a
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



## Register users

To register your users with the **Blockchain Solution Manager** component,
complete the following steps:

TBA - step 2 is only nec. for system users?

1. Authenticate, as **Organization Administrator**, to the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window}. On the
upper right of the interface, click the **Authorize** button and specify your [Bearer Token](glossary.html#bearertoken){:new_window}. With success, you are authorized to call any endpoint in the API.

2. Exchange your Cloud IAM Token for a service Onboarding Token by executing a **POST** call to
the appropriate endpoint for your service connection type: for application connections, call the [/v1/iam/exchange_token/apps/appId ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Programmatic%20OAUTH%20Login%20Flow/post_v1_iam_exchange_token_apps__appId_){:new_window} endpoint; and for
solution connections, call the [/v1/iam/exchange_token/solution/{solutionId}/organization/organizationId ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Programmatic%20OAUTH%20Login%20Flow/post_v1_iam_exchange_token_solution__solutionId__organization__organizationId_){:new_window} endpoint.

3. You can now register your users by specifying the User IDs (human users) and Service IDs (system users) that are registered with your organization's identity service provider. To complete this step for system users
(Service IDs), call the [PUT /v1/organizations/{organizationId}/systems ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Organization%20Systems/put_v1_organizations__organizationId__systems){:new_window} endpoint, where **organizationId** is your Organization ID (the default value is *org1*). Specify your Organization Administrator token, and SolutionId (the default value is *default*). To complete this same step for Human Users (User IDs), call the [PUT  /v1/organizations/{organizationId}/users](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Organization%20Users/put_v1_organizations__organizationId__users) endpoint.

4. Upon user login, the identity service provider redirects to Blockchain Solution Manager to obtain an **Onboarding Token**.

5. The **Onboarding Token** returned by Blockchain Solution Manager is valid, for a limited time,
as proof of identity for the user to interact with the Blockchain Document Store service. (Note that **System Users must first exchange their Onboarding Token for a Reference Token.**

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
