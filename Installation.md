## Download Latest

The required files will be available [here](https://github.com/spsprinkles/message-center/releases) for download.

## SPFx Solution

The application will require you to download the `message-center.sppkg` SPFx package.

### App Catalog

Add the SPFx package to the site collection or tenant app catalog. Deploy the SPFx package and make it available to all immediately.

Note - If you choose not to make it available, then you must add the app manually to the site. [Reference from Microsoft](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/tenant-scoped-deployment)

### Create Page

Access the site to store the message center items. Click on `New` and then `Page` to create a new modern page. Configure the page and click on the `+` icon to add a webpart. Find the `Message Center` app under the `Advanced` section.

### Install Lists

On initial load of the app, it will show you the installation dialog for creating the list. Click on `Install` to create the list.

#### Security

Once the list is installed, the security dialog will be displayed. This app will utilize the default site owners, members and visitors group to control access to the app. By default, it will inherit the permission from the site. Click on `Configure` to break inheritance and set the default owners, members and visitors groups to the app. Click on `Refresh` to reload the page.

#### Publish Page

Review the webpart configuration options and save/publish the page.

## Flows

### Overview

The application uses two flows to add items to the SharePoint list and cleanup items older than 60 days. Download the appropriate files for your environment.

#### Default Environment

* MessageCenter.zip
* MessageCenterCleanup.zip

#### DoD Environment

The DoD packages will target the appropriate graph endpoints.

* MessageCenterDoD.zip
* MessageCenterCleanupDoD.zip

#### Requirements

The flow will require an application registration with the following permissions to the Graph API:

* ServiceHealth.Read.All

### Import Flow Package

Access your flow environment. Click on `My flows` from the left navigation. Once the page loads, click on `Import Package (Legacy)` to import the flow to your environment. You will need to complete the following for both of the flow packages.

#### Select File

Click on `Browse` and select the flow package you downloaded.

#### Import Setup

The import setup will default to `Create as new`. If you are updating an existing flow, then click on the link to change the option to `Update`.

#### Connections

Click on the `Select during import` links for the connectors, and select the account.

#### Import Flow

Click on `Import` to add/update the flow to your environment.

### Update SPFx Configuration

Note the `Message Center` flow id and update the SPFx webpart configuration with this information.

### Configure Flows

Each flow will need to be configured for your environment.

#### Message Center Flow

This is a recurrence flow. It requires an app registration in 

##### Recurrence

The default is set to run at `10PM every day`.

##### Set Client ID

Set the client id from the app registration.

##### Set Client Secret

Set the client id from the app registration.

##### Set Tenant ID

Set the client id from the app registration.

##### Get Access Token to Graph

Review the scope value and ensure it's targeting the correct graph api endpoint for this tenant.

##### Get Message Item

Set the web url and list created by the SPFx app.

##### Create Item

Set the web url and list created by the SPFx app. By default the new items will set the `Is Approved` field value to `false`. A notification will be sent when new items are created for approval. You can adjust this setting if you want to make all items available to the users.

##### Update Item

Set the web url and list created by the SPFx app.

##### Send an email (V2)

Set the email(s) for any new items created notification.

#### Message Center Cleanup Flow

##### Recurrence

The default is set to run at `10PM every day`.

##### Get Items

Set the web url and list created by the SPFx app. The query is set to find items older than `60 days`. If you need to adjust this value, you will need to update the format date time function.

##### Delete Item

Set the web url and list created by the SPFx app.