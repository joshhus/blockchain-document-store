---

copyright:
  years: 2018
lastupdated: "2018-05-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{:shortdesc}

# Manage networks
tba
Once you have provisioned the IBM Blockchain Document Store service,
you will register your IBM Blockchain network, solution and applications with
IBM Blockchain Solution Manager. You can also use this process to modify a
registered network, solution or application.

**Authority/Role**: Member Organization [Network Administrator](glossary.html#network-administrator){:new_window} and [Solution Administrator](glossary.html#solution-administrator){:new_window}

## Register or modify a network
An authenticated Service Administrator for each member organization must register
their organization's instance of the Blockchain Document Store service with an
IBM Blockchain network, as follows:

**Attention**: The *service-onboarding-basepath* is unique per organization; see your
blockchain network service provider.  

1. Copy your Blockchain Document Store **Onboarding Token** from
*service-onboarding-basepath*/onboarding/v1/logins.
2. Using the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window},
open a PUT request to the **/onboarding/v1/networks** endpoint, and paste your **Onboarding Token** from Step 1 into the **Authorization Header**.
3. Return to your *service-onboarding-basepath* and copy your network configuration JSON from the **Blockchain Credentials** tab.
4. Return to the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window},
and paste your network configuration JSON, as shown in [IBM Blockchain network configuration - JSON example](configure-json-example.md), into the **Body** of your **PUT /onboarding/v1/networks** call.

## Register or modify a solution
An authenticated Solution Administrator for each member organization must register their organization's instance of the Blockchain Document Store service with the network applications, as follows:

**Attention**: The *service-onboarding-basepath* is unique per organization; see your blockchain network service provider.  

1. Copy your Blockchain Document Store **Onboarding Token** from *service-onboarding-basepath*/onboarding/v1/logins.
2. Using the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window},
open a PATCH request to the **/onboarding/v1/solutions** endpoint, and paste your **Onboarding Token** from
Step 1 into the **Authorization Header**.

## Register or modify an application
An authenticated Network Administrator for each member organization (or an IBM
Blockchain Network Service Provider) must register their organization's instance
of the Blockchain Document Store service with any IBM Blockchain applications that
the service will interact with, as follows:

1. Copy your Blockchain Document Store **Onboarding Token** from
https://*service-onboarding-basepath*/onboarding/v1/logins.
**Note**: The *service-onboarding-basepath* is unique per organization; see your blockchain network service provider.  
2. Using the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window},
open a PUT request to the **/onboarding/v1/apps** endpoint, and paste your JSON Web Token into
the **Authorization Header**.
3. Create your application service JSON, and paste it into the **Body** of a **PATCH /onboarding/v1/apps** call. For example:
    ```
    {
    "applications": [
      {
        "appId": "string",
        "appName": "string",
        "roles": [
          "SM_SOLUTION_READER"
        ],
        "services": [
          {
            "serviceId": "string",
            "isBlockchainClient": true
          }
        ]
      }
    ]
  }
    ```

## Query an application

You can query an application to check the application definitions. To return a list
of all defined applications, leave the appId parameter blank. For an application to
be searchable, it must include the SM_SOLUTION_READER role definition:

1. From the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window},
open a GET request to the **/onboarding/v1/apps/{appId}** endpoint, and paste your **Onboarding Token** into
the **Authorization Header**.
2. Paste the application *appId* into the **Body** of the GET request, for example:
    ```
    {
"ok": true,
"statusCode": 0,
"response": {
  "appId": "string",
  "appName": "string",
  "roles": [
    "SM_SOLUTION_READER"
  ],
  "services": [
    {
      "serviceId": "string",
      "isBlockchainClient": true
    }
  ]
}
}
    ```

## What's next?
Proceed to [Manage users](manage-users.html).
