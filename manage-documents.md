---

copyright:
  years: 2018
lastupdated: "2018-03-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Manage documents
The Blockchain Document Store service supports the following document management
tasks: upload, download, view, share, verify and replace. The service supports
two document types: **Files** and **JSON**. **Files** are digital documents
in common formats, such as PDFs, text, JSON, spreadsheets, images and
multimedia, uploaded to blockchain network object storage. In addition to being
uploaded as files, **JavaScript Object Notation (JSON) documents** can also be uploaded
directly to the blockchain ledger, in the body of an API call.

**Attention**: Calling a Blockchain Document Store API requires submitting the *chaincode_id*
for the user's member organization. The *chaincode_id* authorizes user actions to be
recorded on the channel ledger.

**Authority/Role**: Member Organization Registered User  
**API overview documentation**: [Blockchain Document Store APIs](docstore-api.html)  
**Swagger interface**: [Blockchain Document Store APIs ![External link icon](images/launch-glyph.svg "External link icon")](https://stage.pbsa-dev1.us-south.containers.mybluemix.net/docstore/swagger-ui.html.){:new_window}.

## Upload documents
The Blockchain Document Store service enables any authenticated user on a
network channel to upload two types of documents: **Files** and **JSON**. The service
uploads **Files** to IBM Cloud Object Storage for secure, permissioned access,
by channel. File attributes, including document ID (*doc_id*), version (*doc_version*)
and metadata, are written to the blockchain ledger as a transaction record,
permanently linking them to the stored file. Any subsequent user action taken against
a document is recorded on the channel ledger, as a new transaction.

To upload a **new document**, call an [Upload](docstore-api.html#Upload) **POST** endpoint; to
**replace an uploaded document**, call an [Upload](docstore-api.html#Upload) **PUT** endpoint.
Note that JSON documents can be uploaded either to the blockchain ledger, in the
body of an API call, or to IBM Cloud Object Store, as a text file.

## Download documents
The Blockchain Document Store service enables any authenticated user on a network
channel to download (and view) documents (Files and JSON) that have been uploaded to
the channel by the service. Call [Download](docstore-api.html#download) endpoints to download
documents (Files and JSON), by organization *chaincode_id* and document *doc_id*.

## Share documents
The Blockchain Document Store service enables any authenticated user on a network
channel to share uploaded documents (Files and JSON) with another authenticated
user on the channel. [Share](docstore-api.html#Share) endpoints create document URLs to send
to other users on the channel documents, and download records of share actions,
by organization *chaincode_id* and document *doc_id* and *doc_version*.

## Verify documents
The Blockchain Document Store service enables any authenticated user on a
network channel to verify documents (Files and JSON) that have been uploaded
using the service. To verify a document, the service compares two upload
transactions, for the same file, on the blockchain ledger. [Verify](docstore-api.html#verify)
endpoints perform an upload of the document being verified, and a compare the
document *file* and *doc_id* values on the channel ledger. Alternatively, an
authenticated user can upload a file as a new document, with a **receipt**,
and the service compares the hash values on the ledger and returns the result.

## Replace documents
The Blockchain Document Store service uploads two types of documents: **Files**
and **JSON**. To replace a document, you must call an [Upload](docstore-api.html#upload) **PUT**
endpoint. (To upload **new documents**, call an [Upload](docstore-api.html#upload) **POST** endpoint.)
The service uploads **Files** to IBM Cloud Object Storage for secure, permissioned
access, by channel. File attributes, including document ID (*doc_id*),
version (*doc_version*) and metadata, are written to the blockchain ledger as a
transaction record, and permanently linked to the stored file. Any subsequent user
action taken against an uploaded document (File or JSON) is recorded on the channel
ledger as a new transaction.

A JSON document can be uploaded to the blockchain ledger
in the body of an API call, or uploaded to object store as text **File**. To
replace JSON on the ledger, submit a **/json** API call with the same *doc_id* and
new JSON content in the API body. To replace JSON that has been uploaded to
object store as a text **File**, use the file replacement method.

**Attention**: No data or files are ever overwritten or deleted from the blockchain ledger,
or from object store. "Replacing" a document merely uploads a newer version of the
document. The newer version of a File or JSON is added to the network, with
the same *doc_id* and an incremented *doc_version*.

## States
The Blockchain Document Store service enables any authenticated user on the network
channel to view the [States](docstore-api.html#states) of uploaded documents and pending document
transactions, and change (i.e. update) **user-defined** states only, of documents.
**System-defined** states of documents cannot be explicitly changed by user actions.

## Additional API calls
For additional Blockchain Document Store capabilities, call the following API
endpoints, at [Blockchain Document Store API ![External link icon](images/launch-glyph.svg "External link icon")](https://stage.pbsa-dev1.us-south.containers.mybluemix.net/docstore/swagger-ui.html){:new_window}:
- Call [Access log](docstore-api.html)#access-log) endpoints to view document access records
- Call [Documents)](docstore-api.html#documents) endpoints to search for specific documents
- Call [Version](docstore-api.html#version) endpoints to view the history of document versions

## Document management API
The [Blockchain Document Store API ![External link icon](images/launch-glyph.svg "External link icon")](https://stage.pbsa-dev1.us-south.containers.mybluemix.net/docstore/swagger-ui.html){:new_window},
for managing documents, is shown below in Figure 1. Once you are logged in to the API interface,
click any **Expand Operations** link to view the details for each endpoint, including **Model**,
**Model Schema**, **Parameters** and **Response Messages**.

## API endpoints
Use the Blockchain Document Store API endpoints to manage documents:

- [API endpoints](solution-manager-api.html)
- [Swagger API interface ![External link icon](images/launch-glyph.svg "External link icon")](https://stage.pbsa-dev1.us-south.containers.mybluemix.net/docstore/swagger-ui.html){:new_window}.
To use an endpoint, click **Expand Operations**.
