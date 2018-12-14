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

# Connect as solution

Connecting your Blockchain Document Store instance to a network as a **blockchain
solution** is recommended for organizations that require individual,
user-level attribution for each blockchain transaction. Under the solution
model, each transaction recorded on the blockchain ledger is attributed to an
authorized user and a registered organization.

To connect Blockchain Document Store as a blockchain solution, complete the following steps:

1.  Using the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/UI%20OAUTH%20Login%20Flow/get_v1_logins){:new_window}, execute a **GET** call to the  *service-onboarding-basepath*/onboarding/v1/logins endpoint. Copy your Blockchain Document Store **Onboarding Token** (JSON Web Token - JWT).

**Attention**: The *service-onboarding-basepath* is unique per organization; see your blockchain network service provider.  

2. Using the [Blockchain Solution Manager API ![External link icon](images/launch-glyph.svg "External link icon")](https://dev.pbsa-dev1.us-south.containers.mybluemix.net/onboarding/swagger/#/Solution/get_v1_solutions){:new_window},
execute a **PATCH** call to the *service-onboarding-basepath*/onboarding/v1/solutions  endpoint. Paste your **Onboarding Token** from Step 1 into the **Authorization Header**.

3. Create your solution definition JSON, and paste it into the **Body** of the **PATCH** call to the /onboarding/v1/solutions endpoint. For example:
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
