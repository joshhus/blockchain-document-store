---

copyright:
  years: 2018
lastupdated: "2018-12-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# System user authentication

**Blockchain Document Store** authenticates system users through the following interactions. System users authenticate through the IBM Cloud IAM **iam.ng.bluemix.net/oidc/token** endpoint and then exchange their **IBM Cloud IAM Token** for a service **Onboarding Token**, as follows:

1. A **Solution Administrator** for the organization <a href="register-app.html#createsvcid">creates an IBM Cloud IAM Service ID</a> for the system user.

2. The system user authenticates through the IBM Cloud IAM endpoint and requests an **IBM Cloud IAM Token** by API key:
    ```
    curl -v -u "demo:demo" -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=$USER_API_KEY" "https://iam.ng.bluemix.net/oidc/token"   > iam.apikey.token
    ```
3. The system user specifies the received **IBM Cloud IAM Token** in the **Authorization Header** of a request for an **Onboarding Token**, which is passed to **Blockchain Solution Manager** for verification and decoding into human-readable strings:

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
