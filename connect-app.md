---

copyright:
  years: 2018
lastupdated: "2018-12-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{:shortdesc}

# Connect as application

Connecting your Blockchain Document Store service instance as an **application**
is recommended for organizations that will use a single entity, such as a third-party
broker, to execute blockchain transactions on behalf of their organization. Under
this broker model, transactions executed and recorded on blockchain for the
organization are attributed to the broker. To connect your service instance as
an application, your organization must have no need to distinguish blockchain
transactions between individual and group user IDs.

To configure Blockchain Document Store as an application, complete the following
steps:

1.  Using the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/UI%20OAUTH%20Login%20Flow/get_v1_logins){:new_window}, execute a **GET** call to the  *service-onboarding-basepath*/onboarding/v1/logins endpoint. Copy your Blockchain Document Store **Onboarding Token** (JSON Web Token - JWT).

**Attention**: The *service-onboarding-basepath* is unique per organization; see your blockchain network service provider.  

2. Using the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Apps/put_v1_apps){:new_window}, execute a **PUT** call to the *service-onboarding-basepath*/onboarding/v1/apps endpoint, and paste your **Onboarding Token** into the **Authorization Header**.

3. Create your application definition in JSON, and paste it into the **Body** of a **PATCH** call to the /onboarding/v1/apps** endpoint. For example:
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

1. From the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Apps/get_v1_apps){:new_window},
execute a **GET** call to the *service-onboarding-basepath*/onboarding/v1/apps endpoint, and paste your **Onboarding Token** into the **Authorization Header**.

**Attention**: The *service-onboarding-basepath* is unique per organization; see your blockchain network service provider.  

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
