# PureCloud API test application for creating a dummy outbound contact list

This repository contains code for a static web site that can be embedded inside PureCloud to process API tests.
This is provided as developped by Orange Business Services as an example of a frontend calling the PureCloud API.
It is inspired by PureCloud GDPR Requests App (https://github.com/purecloudgdprrequests/purecloudgdprrequests.github.io).

**PLEASE NOTE: This is not an official Genesys or Orange Business Services application**

**Do not send requests to Genesys or Orange Business Services Customer Care about this application**

## How to embed in PureCloud

To configure the application, you need to create a new `Token Implicit Grant (Browser)` OAuth entry in your PureCloud org
    * Go to Admin/OAuth
    * Click on `Add Client`
    * Give it a meaningful name (e.g. `Outbound dummy contact list creation`)
    * Description is optional
    * Set the grant type to `Token Implicit Grant (Browser)`
    * In `Authorized redirect URIs`, enter the URL to reach the `index.html` file (see `Start a web server` section for more info)
    * Click on `Save` and note the `Client ID` string value
* Edit the `static/js/purecloud.js` file and update the following variables with your own PureCloud credentials
    * clientId: The new OAuth Client Id you just generated
    * redirectUrl: Corresponds to the full URL to your index.html and must be the same than the one you set in the OAuth credentials above (e.g. `https://boborangesam.github.io/dummyContactList.github.io/apicall.html`)
    * environment: Either `mypurecloud.ie`, `mypurecloud.de`, `mypurecloud.com`, `mypurecloud.com.au` or `mypurecloud.jp` depending on where your PureCloud org is located

To embed the resulting web site directly inside PureCloud, you need to create a new `Integration`

* Go to `Admin/Integrations` and click on `+Integrations` on the top right to add a new client application
* In the `Details` tab:
    * Enter a name for the new client application
* In the `Configuration` tab, enter the following:
    * Application URL: The full path to your site (e.g. https://boborangesam.github.io/dummyContactList.github.io/apicall.html)
    * Application Type: stand-alone or widget, as you wish. Widgets are best for agents-facing apps, stand-alone are best for administrators' tasks.
    * Application Category: (leave empty)
    * Iframe Sandbox Options: allow-scripts,allow-same-origin,allow-forms,allow-modals (default value)
    * Group Filtering: Select a group of users who can access this client application. You might have to create a new group first in `Admin/Groups`
    * Click on `Save`
* Go back to the `Details` tab and click on `Active` to activate this application
