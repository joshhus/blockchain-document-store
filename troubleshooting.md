---

copyright:
  years: 2018
lastupdated: "2018-03-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Troubleshooting

Before contacting IBM Blockchain Document Store support, you can search the
error messages and resolutions below. You can also review the API documentation.

## Error messages

IBM Blockchain Document Store error messages and troubleshooting steps are provided
below:

----------

**Message**: 400 (Bad request)

`blockchain-document-store.doc-persistence.400-bad-request-error`

**Symptom**: A Blockchain Document Store API returns a **400 (Bad request)** error message.
The **200 OK** message is expected.

**Explanation**: This message indicates that the request is not formatted correctly. The body
of the message indicates the problem:
- A missing required field.
- An improperly formatted value (such as a string instead of a number).
- Incorrectly formatted JSON.
- Other problem.

**Action**: Review the Blockchain Document Store API documentation for the required syntax, and resubmit the call.

----------

**Message**: 400 (Could not parse...)

`blockchain-document-store.doc-persistence.400-bulk-upload-error`

**Symptom**: The **POST /v1/docstore/{instance_id}/documents** API
returns a **400** error message: `400 Could not parse multipart servlet request; nested exception is java.io.IOException:org.apache.tomcat.util.http.fileupload.FileUploadException: the request was rejected because
no multipart boundary was found`. The **200 OK** message is expected.

**Explanation**: The API expects **MultipartHttpServletRequest** as the body type, but Swagger does not
support uploading files with this body type.

**Action**: Use Postman instead of Swagger to upload multiple documents:
1. If necessary, download and configure Postman, from https://www.getpostman.com/.
2. Select **POST** from the Postman dropdown menu.
2. Enter the application URL; e.g. for the Swagger URL https://*app-url*/docstore/swagger-ui.html, specify the Postman URL https://*appurl*/docstore/v1/docstores/instance_id/<*end_point*>.
3. Select `form-data` as the body type.
4. Add types and documents. Each document can be either a File or JSON.

----------

**Message**: 401 (Unauthorized)

`blockchain-document-store.doc-persistence.401-error`

**Symptom**: A Blockchain Document Store API returns a **401 (Unauthorized)**
error message. The **200 OK** message is expected.

**Explanation**: An unauthorized user has attempted an API call:
- The user may not be authorized to use Blockchain Document Store.
- The user may not have provided a valid token for an API call.
- The user may have provided an expired token; the default length is 3 hours.

**Action**: The most common reason for this error message is the user calling an API without a
valid security token. Try the following steps, as applicable, to address the problem:
- In Swagger, replace the Bearer 'access_token' with the user's JSON Web Token (JWT). Do **not** click **Explore** or **Enter** after replacement.
- In Postman, add `Bearer *access_token*` to an Authorization header and resubmit
the API call.
- If the error message persists, obtain a new JSON Web Token (JWT) and try again.

----------

**Message**: 404 (Not found)

`blockchain-document-store.doc-persistence.404-document-not-found-error`

**Symptom**: An uploaded document (JSON or File) cannot be downloaded successfully.
The **200 OK** message is expected.

**Explanation**: A **404** response indicates that the document (File or JSON)
is not found on the network. The upload transaction could still be pending,
or the request has a problem:
- A missing required field.
- An improperly formatted value (such as a string instead of a number).
- Incorrectly formatted JSON.
- Other problem.

**Action**: Try the following actions to correct the download problem:
1. Check the status of the *correlation_id* for the upload of the document.
If the status is not `success`, the upload transaction is still in progress.
2. Verify that the requested *doc_id* and *doc_version* values are correct.
3. Verify that the request format is correct.

---------

**Message**: 500 (JSON Receipt Verification Error)

`blockchain-document-store.doc-persistence.500-json-receipt-verification-error`

**Symptom**: A call to the **POST /v1/docstores/{instance_id}/documents
/json/receipt_verifications** API returns a **500 (JSON Receipt Verification Error)**
 message. The **200 OK** message is expected.

**Explanation**: To verify a JSON document on blockchain using the receipt method,
the API expects a request body of type `form-data`, but the Swagger send type is
`application/x-www-form-urlencoded`.

**Action**: Use Postman instead of Swagger to verify JSON with a receipt:
1. If necessary, download and configure Postman, from https://www.getpostman.com/.
2. Select **POST** from the Postman dropdown menu.
3. Enter the application URL; e.g. for the Swagger URL https://*app-url*/docstore/swagger-ui.html, specify the Postman URL  https://*appurl*/docstore/v1/docstores/instance_id/<*end_point*>.
4. Select `form-data` as the body type.
5. Add an Authorization header.
6. Add the document receipt and json_content as key-value pairs in body.

---------

**Message**: 500 (Internal Server Error)

`blockchain-document-store.doc-persistence.500-internal-server-error`

**Symptom**: A Blockchain Document Store API call returns a **500 (Internal
  Server Error)** message. A **200 OK** message is expected.

**Explanation**: This error message typically indicates an issue with the
blockchain client and its communication with IBM Blockchain Solution Manager, or
a problem with the connection to the blockchain network.

**Action**: Check for connectivity issues:
1. Check the client connection to your IBM Blockchain network.
2. Check the client connection to the IBM Blockchain Document Store solution manager.
3. If the problem persists, contact [IBM Blockchain Document Store support](https://www.ibm.com/mysupport/s/topic/0TO500000001y2FGAQ/food-trust?language=en_US&productId=01t50000004XBJaAAO).
