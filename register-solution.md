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

# Register a solution

Registering a solution with the **Blockchain Document Store** service enables individual and group users, in a registered organization, to transact on a blockchain network. Under this solution model of accessing the network, each
transaction recorded on blockchain is attributed to an individual or group.

**Prerequisites:**  To register a solution, first meet the prerequisites in the following sequence:
1. Complete the **connect to a member** steps  
2. Authenticate as **Network Administrator**  

## Register solution

Complete the following steps to register your solution with the **Blockchain Document Store** service:

1. **Retrieve Network Administrator Onboarding Token**: Execute a **GET** call to the ** *service-onboarding-basepath*/v1/logins ** endpoint. Copy your **Onboarding Token** from the returned message. **Attention**: The ** *service-onboarding-basepath* ** is unique per member Organization.

2. **Paste Token**: Execute a **PATCH** call to the ** *service-onboarding-basepath*/v1/solutions ** endpoint. Paste your **Onboarding Token** from Step 1 into the **Authorization Header** of the request. Continue with Step 3 to complete this **PATCH** call.

3. **Create Solution Definition JSON**: Create your **solution definition JSON**, and paste it into the **Body** of the **PATCH** call to the ** *service-onboarding-basepath*/v1/solutions ** endpoint. For example:
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

4. Submit the request via POST or Curl command.

## What's next?
Proceed to [human user authentication](auth-user.html) or [system user authentication](auth-system.html).
