---

copyright:
  years: 2018
lastupdated: "2018-12-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{:shortdesc}

# Access as solution

Accessing your **Blockchain Document Store** instance as an **IBM Blockchain solution**
is recommended for organizations that require individual, user-level attribution for
each blockchain transaction. Under this **solution model**, each transaction recorded on
the blockchain ledger is attributed to an authorized user of a registered organization.

To configure access to **Blockchain Document Store** as an **IBM Blockchain solution**,
complete the following steps:

1.  Retrieve your service **Onboarding Token** by executing a **GET** call to the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/){:new_window} ** *service-onboarding-basepath*/onboarding/v1/logins ** endpoint. Copy your **Onboarding Token** from the returned message. **Attention**: The ** *service-onboarding-basepath* ** is unique per organization; see your blockchain network service provider.

2. Using the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Solution/patch_v1_solutions){:new_window},
execute a **PATCH** call to the ** *service-onboarding-basepath*/onboarding/v1/solutions ** endpoint. Paste your **Onboarding Token** from Step 1 into the **Authorization Header** of the request. Continue with Step 3 to complete this **PATCH** call.

3. Continuing with the same **PATCH** call from Step 2, to the ** *service-onboarding-basepath*/onboarding/v1/solutions ** endpoint, create your **solution definition JSON**, and paste it into the **Body** of the request. For example:
    ```
    {
  "onboardingdata": {
    "solution": {
      "id": "string",
      "name": "string",
      "metadata": {}
    },
    "organizationTypes": [
      {
        "id": "org_id1",
        "name": "string",
        "solutionId": "string",
        "onboardedBy": "string",
        "metadata": {},
        "roles": [
          "role_id234"
        ]
      }
    ],
    "roles": [
      {
        "id": "role_id234",
        "name": "string",
        "solutionId": "string",
        "onboardedBy": "string",
        "isBlockchainRole": true,
        "policies": {}
      }
    ],
    "organizations": [
      {
        "id": "org_id1",
        "name": "string",
        "solutionId": "string",
        "blockchainUserMode": "user | organization | role",
        "organizationTypes": [
          "list of organizationType Ids"
        ],
        "walletManagerURL": "string",
        "metadata": {}
      }
    ],
    "users": [
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
    ]
  }
}
    ```


## What's next?
Proceed to [Manage users](manage-users.html).
