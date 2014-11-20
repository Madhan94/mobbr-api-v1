API V1
======

The Mobbr REST-API documentation.

Mobbr is a payment system for social collaboration and crowd-sourcing. It support crowd-funding with a single button and crowd-payments with a single button.

The API accepts the following payment destinations:
- usernames, email addresses and supported OAUTH user profiles (such as Github, Stackoverflow)
- JSON payment scripts that lists the payment properties and all recipients and their shares
- URL's, in which case the API does a callback to retrieve a JSON payment script from the <metadata name="participation" content="..." /> HTML tag

CONCEPTS
--------
- TASK, is an URL that received a payment of pledge
- RECIPIENT, is an user that receives money
- SENDER, is an user that sends or pledges money
- PARTICIPANT, is an user that participates in a social collaboration


REQUEST FORMAT
--------------

PUT and POST requests can be done in application/xml, application/json and application/x-www-form-urlencoded format. Use the Content-Type header to control this.

GET and DELETE parameters require url encoding for arguments. Arrays are repetitions of same-name-arguments.

    GET /api_v1/invoices?payment_ids=1&payment_ids=2&...

If the Content-Type header is not recognized or permitted the server returns a '406 Not acceptable' response.

RESPONSE FORMAT
---------------

Responses can be requested in application/xml and application/json, use the Accept header for this.

If the Accept header is not recognized or permitted the server returns a '406 Not acceptable' response.

AUTHENTICATION
--------------

Clients and other servers can use HTTP BASIC AUTHENTICATION with each request that needs authentication.

To keep browser apps from storing username/password combinations in possible unsafe places (cookies or local storage) we also provide a second mechanism for authentication: a call to /api_v1/user/password_login returns a temporary access token (result['token']). Use this token as the password for the HTTP BASIC AUTHENTICATION and leave the username empty.

PAGINATION
----------

Lists are limited to 100 items default. To retrieve more items, use the pagination parameters offset and limit. To retrieve 30 items from a list starting at item 10, use &limit=30&offset=10 in the API-call.

SPECIAL API URL'S
-----------------

- The event hook you can attach to your Github repos

    /callback/github

- Button image for specified URL

    /button/<md5_of_url>[/<small|slim|medium|large>[/<currency_iso>]]

- Badge image for specified host/domain (a badge show the totals of an entire site)

    /badge/<protocol>/<host>

OUR OPEN-SOURCE CLIENT
----------------------

Our own website (the AngularJS browser-client) is available as open-source on /mobbr/mobbr-frontend. You can use it to build your own payment website on your own domain. In the Mobbr philosophy everybody who adds value, should receive his or her fair share, so it whould only be logical that you include yourself in the recipients / participants of the transactions you facilitate, taking your fair share.

TEST-ENVIRONMENT / SANDBOX
--------------------------

We have a sandbox available on https://test-api.mobbr.com (API) and https://test-www.mobbr.com (WWW). The sandbox-API uses the Mangopay sandbox and Bitcoin testnet, so you can try anything you like without any risk. The sandbox also doubles as our test-environment so it will not be as stable as our production environment and we reserve the right to reset the database (i.e. clear all accounts) at any time.

Use the following accounts to login to the test environment, usernames TEST1 to TEST10, password: m0bbr2014

The test system will never send mail except for registration mail.

To use the sandbox in your website, just include the mobbr-script from the sandbox-URL (https://test-www.mobbr.com/mobb-button.js) instead of the production-URL (https://mobbr.com/mobbr-button.js).

