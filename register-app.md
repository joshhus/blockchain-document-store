---

copyright:
  years: 2018
lastupdated: "2018-12-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{:shortdesc}

# Register an application

Registering an application with the **Blockchain Document Store** service enables
a third-party application to transact on the defined blockchain network. Under this
application model of accessing the network, each transaction recorded on blockchain
is attributed only to the application. No blockchain transactions are attributed
to individual or group users of the registered application.

**Prerequisites:**  To register an application, first meet the prerequisites in the following sequence:
1. Complete the **connect to a member** steps  
2. [Create Service ID](#create-service-ID) for the application  
3. Authenticate as **Network Administrator**  

<a name="createsvcid"></a>

## Create Service ID

To register an application with the Blockchain Document Store service, you must first create an **IBM Cloud IAM Service ID** for the application, as follows:

1. Log in to your [IBM Cloud Resource Dashboard ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){:new_window}.

2. Click on your instance of the **Blockchain Document Store** service.

3. From the **TOP menu bar**, select the **Manage > Security > Identity and access** option.

4. The **Users** page for the account will load by default; in the left pane, click on the **Service IDs** tab.

5. Click the **Create +** button on the right to create a new Service ID; you **must copy and save the value of the Service ID** (e.g. ServiceId-3bf785-449c-422-afd9-12db3913b).

6. On the **Manage Service ID** page, click the **API keys** tab.

7. Click the **Create +** button on the right to create an API key (password) for the Service ID. Enter a **Name** and a **Description**, and click **Create**. You **must copy and save the API key manually** in a secure location.

Now that your application has an IBM Cloud Service ID, you are ready to register the application with the **Blockchain Document Store** service.

## Register application

Complete the following steps to register your application with the **Blockchain Document Store** service:

1. **Generate a Network Administrator Onboarding Token**: Execute a **GET** call to the **  *service-onboarding-basepath*/v1/logins ** endpoint. Copy and save the Blockchain Document Store **Onboarding Token** from the response message. **Attention**: The ** *service-onboarding-basepath* ** is unique per member organization.

2. **Paste API Key**: Execute a **PUT** call to the ** *service-onboarding-basepath*/v1/apps ** endpoint. Paste your **Onboarding Token** from Step 1 into the **Authorization Header** of the request. Continue with Step 3 to complete this **PUT** call.

3. **Create Application Definition JSON**: Create your application definition in JSON. For the application to search users, systems, and organizations, include the **SM_SOLUTION_READER** role. For example:

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

4. Paste your application definition JSON into the **Body** of the **PUT** call to the ** *service-onboarding-basepath*/v1/apps ** endpoint, and submit the request via POST or Curl command.


## What's next?
Proceed to [authenticate the application](auth-app.html).
