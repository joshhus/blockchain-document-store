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


# Application authentication (programmatic)

**Blockchain Solution Manager** authenticates applications only (not other system users) through
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

Applications can include a policy definition, via the  [/v1/apps/{appId}/policy](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/) endpoint, to grant access to users, roles, organizations and other applications. Any application accessing Blockchain Solution Manager must include the **SM_SOLUTION_READER** static variable.

## What's next?
Proceed to [Manage documents](manage-documents.html).
