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


# System user authentication (programmatic)

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

## What's next?
Proceed to [Manage documents](manage-documents.html).
