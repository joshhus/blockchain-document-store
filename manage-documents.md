---

copyright:
  years: 2019
lastupdated: "2019-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Manage documents

The **Blockchain Document Store** service enables organizations and their users
to easily manage and share all classes of business documents on a blockchain network,
such as purchase orders, advanced shipping notices, and multi-lateral contracts.
Registered and authenticated users can upload, download, view, share, verify,
delete, and replace documents in any format.

Blockchain Document Store **files** are
digital documents uploaded and stored in an object storage database, such as IBM
Cloud Object Store. Documents in JSON format can additionally be uploaded and
stored directly on the blockchain ledger.

## Document management API
The Blockchain Document Store API is provided for all of your document management tasks. Click on any endpoint to view the
the usage details, including the **Model**, **Model Schema**, **Parameters** and **Response Messages**.

## Upload documents
Any authenticated user can upload the two types of documents: **files** and **JSON**.
**Files** are uploaded to an object store database, such as
[IBM Cloud Object Storage ![External link icon](images/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/object-storage/solutions){:new_window}, for secure,
permissioned access, by network channel. JSON documents are uploaded directly to the
blockchain ledger. User-specified attributes for each file, such as metadata, document
ID, and document version, are written to the blockchain ledger as a permanent transaction
record. Any subsequent user action specifying an an uploaded document (File or JSON) is
also recorded on the ledger, as a new transaction.

To **upload a new document**, execute a **POST** call to an **Upload** endpoint. To **replace a stored document**, execute a **PUT** call to an **Upload** endpoint.

A JSON document can be uploaded to the blockchain ledger in the body of an API call,
**OR** to IBM Cloud Object Store as text **File**. To replace JSON on the ledger, submit
a **/json** API call with the same *doc_id* and new JSON content in the API body.
To replace JSON that has been uploaded to object store as a text **File**, use the
file replacement method.

**Attention**: No data or files are ever overwritten or deleted from the blockchain ledger,
or from object store. "Replacing" a document merely uploads a newer version of the
document. The newer version of a File or JSON is added to the network, with
the same *doc_id* and an incremented *doc_version*.

## Download documents
The Blockchain Document Store service enables any authenticated user on a network
channel to download (and view) documents (Files and JSON) that have been both uploaded
by the service and shared with the user's Organization. Call the Download API endpoints
to download documents (Files and JSON), by *chaincode_id* and *doc_id*.

To **download a document**, execute a **GET** call to a **Download** endpoint. To **download documents in bulk**, execute a **POST** call to a **Download** endpoint.

## Search documents
The Blockchain Document Store service enables any authenticated user on a network
channel to search documents (JSON only) that have been both uploaded by the
service and shared with the user's Organization. Call the Search API endpoint to
search JSON documents, by *doc_type*, time range, JSON content, and *channel_id*.

To **search a document**, execute a **POST** call to the **Search** endpoint.

## Share documents
The Blockchain Document Store service enables any authenticated user on a network
channel to share uploaded documents (Files and JSON) with other authenticated
users on the channel. Call a **Sharing** endpoint to create document URLs to share
with other users on the channel, download
shared documents, and download records of share actions, by *chaincode_id*, *doc_id*, and *doc_version*.

## Verify documents
The Blockchain Document Store service enables any authenticated user on a
network channel to verify documents (Files and JSON) that have been uploaded
using the service. To verify a document, the service compares two upload
transactions, for the same file, on the blockchain ledger. Call the **Verification** endpoints to perform an upload of the document being verified, and compare the
document *file* and *doc_id* values on the channel ledger. Alternatively, an
authenticated user can upload a file as a new document, with a **receipt**,
and the service compares the hash values on the ledger and returns the result. In either case,
the process verifies that your local copy matches the copy on the network.

## Manage states
The Blockchain Document Store service enables any authenticated user on the network
channel to view the states of uploaded documents and pending document
transactions, and change (i.e. update) **user-defined** states only, of documents.
**System-defined** states of documents cannot be explicitly changed by user actions.
Call the **States** endpoints to view and add document states.

## Additional API calls
For additional Blockchain Document Store capabilities, call the following API
endpoints:
- Call **Access log** endpoints to view document access records.
- Call **Documents** endpoints to search for specific documents.
- Call **Version** endpoints to view the history of document versions.
