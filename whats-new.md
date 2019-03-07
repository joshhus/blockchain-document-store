---

copyright:
  years: 2018
lastupdated: "2018-09-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# What's new

**IBM Blockchain Document Store** recent updates are described below:
- v1.0.7 (September 20, 2018)
- v1.0.6 (August 17, 2018)   
- v1.0.5 (August 1, 2018)   
- v1.0.4 (July 19, 2018)  

---------------------------------------

## Version 1.0.7
(2018-09-20)

Doc-Persistence 	|CC-client 	|Onboarding
---- | ---- | ----
0.5.12 	|0.5.7 	|1.2.15

Supports: IBP 1.0.x and IBP 1.1

### Onboarding

No changes from 1.0.6.1

### Doc-Persistence

**1. Bulk Delete:**

Breaking changes to the delete endpoint; now the response will have more details about the status of each document:

`DELETE /v1/docstores/{channel_id}/documents`    

Suppose three documents are to be deleted. Assume doc_2 is already deleted and doc_3 does not exist:

Request Body:

```
{
  "docIds": [
    "doc_1","doc_2","doc_3"
  ]
}
```

Response Body:

```
{
  "status": 202,
  "response": {
    "correlationId": "b99e9aff-803c-43cd-bc1f-7c7211c556f3"
  }
}
```

New Response Body:

```
{
  "correlationId": "b99e9aff-803c-43cd-bc1f-7c7211c556f3",
  "transactionStatus": "in_progress",
  "message": "In progress.",
  "documentStatus": {
    "doc_1": {
      "status": "in_progress",
      "message": "deleting"
    },
    "doc_2": {
      "status": "already_deleted",
      "message": "Document already deleted."
    },
    "doc_3": {
      "status": "not_found",
      "message": "Document not found."
    }
  }
}
```

**Status Codes**  

Transaction Level:  
- `all_documents_failed` : All documents failed with validation errors.
- `all_documents_deleted` : All documents already deleted.
- `in_progress` : In progress.  

Document Level:  
- `already_deleted` : Document already deleted.
- `in_progress` : In progress.
- `not_found` : Document not found.  


**2. New Endpoint Transaction V2**

A new endpoint that enhances the transaction status response is added:

`GET /v2/docstores/transactions`

Every transaction will have a single `transactionStatus` that will reflect if the transaction is failed or succeeded.

The status of the same co-relation endpoint through this new endpoint would be
as follows:

```
{
  "b99e9aff-803c-43cd-bc1f-7c7211c556f3": {
    "transactionStatus": "success",
    "message": "Transaction successfully confirmed on the blockchain.",
    "doc_1": {
      "test_fresh_111": {
        "status": "already_deleted",
        "message": "Document already deleted."
      },
      "doc_2": {
        "status": "success",
        "message": "success"
      },
      "doc_3": {
        "status": "not_found",
        "message": "Document not found."
      }
    },
    "blockchainStatus": {
      "status": "success",
      "message": "Transaction successfully confirmed on the blockchain.",
      "startTime": 1537377220877,
      "endTime": 1537377223140
    }
  }
}
```

**Status Codes**  

Transaction Level:  
- `success` :  Transaction Succeeded
- `failed` :  Transaction Failed
- `in_progress` : In progress
- `not_found` : Transaction not found.

Document Level:  
- `already_deleted` : Document already deleted
- `in_progress` : In progress
- `success` : Operation on document succeeded
- `not_found` : Document not found.

**3. Dependency updates**

Springboot version increased from 1.5.8 to 1.5.15 (stricter check for the
  path variable: `channel_id` in the url).


### CC-client

- Internal change to global IAM endpoint
- Dependency updates
- Ability to override numeric and boolean environment variables (used by the BDS team)


---------------------------------------------

## Version 1.0.6
(2018-08-17)

Doc-Persistence 	|CC-client 	|Onboarding
---- | ---- | ----
0.5.2 	|0.5.4 	|1.2.14

Supports: IBP 1.0.x and IBP 1.1

### Onboarding

Support IBP V 1.1 Enterprise and Starter Plan.  
**Please note:** This release does not support migrating an instance of BDS running on IBP 1.0 to IBP 1.1 - this support is targeted for a future release.

### Doc-Persistence

**1. Bulk Upload Endpoint is Deprecated**

Deprecated Endpoint:

`POST /v1/docstores/{channel_id}/documents`

**2. V2 Bulk Upload/Update Endpoint**

New V2 endpoint for bulk upload of docs is added:

`PUT /v2/docstores/{channel_id}/documents`

**Functionality**

- Both JSON and attached Files can be uploaded
- Documents can be either new or a new version of any existing document (i.e. same DocumentID)
- If document type already exists for the earlier version of doc, the document type will **NOT** be updated even if a new type is provided.  


**Status Codes**  

Transaction Level:  
- `types_invalid_format` : Types map invalid.
- `all_documents_failed` : All documents failed with validation errors.
- `all_documents_deleted` : All documents already deleted.
    in_progress : In progress.  


Document Level:  
- `already_deleted` : Document already deleted.
- `duplicate_entry` : Duplicate document content or files.
- `content_invalid_format` : Document content is not a valid JSON
- `in_progress` : In progress.


**3. Single Hash for JSON Document**

This endpoint generates a JWT (Java Web Token) receipt, which used to contain docHash for File uploads only. Now `docHash` will be a available for both JSON and File uploads:

`GET /v1/docstores/{channel_id}/documents/{doc_id}/receipts`

**Note:** docHash will only be available for new documents uploaded after this release. The existing JSON docs will not have a docHash.

**Hash generation rules:**  
A hash of JSON is generated after applying these rules:

1. Removing spaces
2. Sorting keys (including nested)
3. Normalizing numbers - e.g. 1.00 is treated as 1

Examples of documents that would have the same docHash:

- `{“A”:”B”,”X”:”Z”}` and `{“X”:”Z”,”A”:”B”}`
- `{“A”:”B”,”C”:{“M”:”N”,”O”:”P”}}` and `{"A":"B","C":{"O":"P","M":"N"}}`
- `{“A”: 1}` and `{“A”: 1.00}`

**Note:** The Bulk Download JSON response will also include the docHash.

### CC-client:
- Potential performance improvement for rabbit queueing
- Deal with commits in progress longer than the poll time (optional)
- Chaincode version handling improvements
- Chaincode version and init args set to 1.0.6


---------------------------------------

## Version 1.0.5
(2018-08-07)

Doc-Persistence 	|CC-client 	|Onboarding
---- | ---- | ----
0.4.8 	|0.5.1 	|1.2.10

Supports: IBP 1.0.x and IBP 1.1

### Onboarding

- User objects are missing fields: https://github.ibm.com/pbsa/support/issues/13
- Onboarding token does not indicate if token is for human user or system user; app has to issue two APIs to retrieve proper records: https://github.ibm.com/pbsa/support/issues/28
- 67 posts to /v1/organizations/{organizationId}/administrators can make /v1/logins hang:  https://github.ibm.com/pbsa/solution-identity/issues/567
- Unable to retrieve self role associated with organization administrator: https://github.ibm.com/pbsa/solution-identity/issues/583
- Unable to migrate organizations: https://github.ibm.com/pbsa/support/issues/165
- Features: /v1/verification/certs API to verify all blockchainUserMode=`user` organization users. https://github.ibm.com/pbsa/solution-identity/issues/577  


### Doc-Persistence

**1. API Changes:**

When the document is not found, the API response code and response body is changed:

**Verification API:**  
`POST /v1/docstores/{channel_id}/documents/files/consistency_verifications`    
`POST /v1/docstores/{channel_id}/documents/files/id_verifications`  
`POST /v1/docstores/{channel_id}/documents/json/id_verifications`  
`POST /v1/docstores/{channel_id}/receipts/validation`  
`POST /v1/docstores/{channel_id}/documents/json/receipt_verifications`  
`POST /v1/docstores/{channel_id}/documents/files/receipt_verifications`  

**Sharing API:**  
`GET /v1/docstores/{channel_id}/documents/{doc_id}/receipts`  
`POST /v1/docstores/{channel_id}/documents/shared_documents`

Old Response Code:  
`200`

New Response Code:  
`404`

Old Response Body:

```
{
  "status": 200,
  "response": {
    "status": "not found",
    "docID": "<doc-id>",
    "docVersion": "<doc-version>"
  }
}
```

New Response Body:

```
{
  "status": 404,
  "error": "Document not found."
}
```

**2. Deleted Documents:**

After a document is deleted, subsequent operations such as upload, delete, and verification will fail with the `410` response code. The affected APIs are documented in Swagger.

Response Code:  
`410`

Response Body:  

```
{
  "status": 410,
  "error": "Document is deleted."
}
```

Check out this 3-minute [Demo Video](https://ibm.ent.box.com/s/ht96dvnxcv622cqb4g4kekj4blynq5ew).

### CC-client

- Protection of install/instantiate endpoints
- Robustly handle failures to connect to onboarding or IAM on startup and keep retrying
- Instantiate/upgrade combination endpoint to alleviate issues where chaincode is already instantiated
- Handle when rabbit heartbeat cannot connect


---------------------------------------------------

<a name="v104"></a>
## Version 1.0.4
(2018-07-19)

Doc-Persistence 	|CC-client 	|Onboarding
---- | ---- | ----
0.4.7 	|0.4.6 	|1.2.9

Supports: IBP 1.0.x
### Onboarding

- no changes from 1.0.3.6

### Doc-Persistence

**1. API Changes:**  

- New API DELETE /v1/docstores/{channel_id}/documents is added. One or more documents can be deleted through this API. Once deleted, documents cannot be recovered. All existing versions of the documents will be deleted.

**2. Delete Functionality:**

Once a document is deleted, the following conditions apply:

- The data stored (if any) in IBM Cloud Object Store and Database will be deleted. This applies to all versions of the documents.
- New system state `delete` will be added for the deleted document.
- Deleted docs cannot be searched though `GET /v1/docstores/{channel_id}/documents/search`
- Deleted docs will not be within the scope of `GET /v1/docstores/{channel_id}/documents/ids`
- Upload, Download and most of the subsequent operations will fail.
- Presence and Bulk Presence will respond with status `deleted`
- Upload of deleted doc will respond with HTTP response code `409 - Conflict`
- Validation endpoints will have status as `deleted`
- Only `GET /v1/docstores/{channel_id}/documents/{doc_id}/access_log` and `GET /v1/docstores/{channel_id}/documents/{doc_id}/states` will be accessible

**3. Known Defect:**  

- If one or more document deletions fail, the status can be found in `/v1/docstores/{channel_id}/transactions` as a concatenated string, for example:

`"blockchainStatusMessage": "Transaction successfully confirmed on the blockchain. Error: abc failed with cannot delete the doc as it does no exist"`

This error message to be changed to a JSON for usability.

### CC-client
- Change chaincode version to 1.0.4


## References
Purchase the service: [IBM Cloud Catalog ![External link icon](images/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/catalog/services/blockchain-document-store){:new_window}.

Purchase an IBM Blockchain service plan: [IBM Blockchain Enterprise Membership Plan ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/catalog/services/blockchain){:new_window}.

## What`s next
After purchasing the service on IBM Cloud, start using IBM Blockchain Document Store,
at [Getting Started]((blockchain-document-store/getting-started.html).
