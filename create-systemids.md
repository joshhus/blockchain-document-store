---

copyright:
  years: 2018
lastupdated: "2018-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Create System IDs

Before registering your **System Users**, you must create a unique
IBM Cloud **Service ID** for each system user, as follows:

1. Log in to your [IBM Cloud Resource Dashboard ![External link icon](images/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){:new_window}.
2. Click on **Manage** in the top-right menu bar.
3. Select the **Security > Identity and Access** option.
4. The **Users** page for the account will load by default; click on the **Service IDs** tab
in the left pane.
5. Click **Create +** to create a new Service ID. You must record the value of the Service ID (e.g. ServiceId-3bf785-449c-422-afd9-12db3913b).
6. On the **Manage Service ID** page, click **API keys**.
7. Click **Create +** to create an API key (i.e. password) for the Service ID. Enter a
**Name** and a **Description**, and click **Create**. You must save the API key, in a secure location.
8. Configure each registered system user (and application) to obtain an **Onboarding Token** by calling the /v1/iam/exchange_token/solution/{solutionId}/organization/{organizationId} endpoint (or for applications, the **/v1/iam/exchange_token/apps/{appId}** endpoint).

## What's next?
Proceed to [Manage documents](manage-documents.html).
