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


# Application authentication

The **Blockchain Document Store** service authenticates an application with an IBM Cloud IAM Service ID through the following interactions. Applications authenticate through the IBM Cloud IAM **iam.ng.bluemix.net/oidc/token** endpoint, and then exchange the returned **IBM Cloud IAM Token** for a service **Onboarding Token**, as follows:

1. A **Network Administrator** <a href="register-app.html#createsvcid">creates an IBM Cloud IAM Service ID</a> for the application.

2. The application Service ID authenticates through the IBM Cloud IAM **iam.ng.bluemix.net/oidc/token** endpoint, and requests an **IBM Cloud IAM Token**:

    ```
    curl -v -u "demo:demo" -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=$USER_API_KEY" "https://iam.ng.bluemix.net/oidc/token"   > iam.apikey.token
    ```
3. The application adds the returned **IBM Cloud IAM Token** to the **Authorization Header** of an API request for a service **Onboarding Token**, which it passes to Blockchain Solution Manager for verification and decoding into human-readable strings:
    ```
    curl -k  -H "Content-Type: application/json" --data-binary @iam.apikey.token -X POST "/v1/iam/exchange_token/apps/{appId}"
    ```

4. If verified, the application receives an **Onboarding Token** from Blockchain Solution Manager.

**Note**: The default **Onboarding Token** timeout is three hours.

## What's next?
Proceed to [Manage documents](manage-documents.html).
