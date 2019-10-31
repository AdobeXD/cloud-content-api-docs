# Quick Start: Make your first API call

Let’s walk through making your first XD Cloud Content API call together.

We'll keep things simple in this tutorial and use the command line tool [cURL](https://curl.haxx.se) to make a request call. 

At the end of the tutorial, we'll suggest some next steps for going deeper with the XD Cloud Content APIs.

## Prerequisites

- Basic knowledge of Command Line Interfaces and APIs
- A text editor to write your code in (like VSCode, Sublime Text, Brackets, Atom, etc)

## Development Steps

### 0. Get a client ID and client secret

Before you start, you'll want to request a client ID and client secret by filling out [this form](https://adobe.allegiancetech.com/surveys/JDQ78F/).

If approved, you will be assigned a unique client ID and client secret, which can be used to make API calls.


### 1. Decide whether your app will access private cloud docs or not

XD cloud documents are either private or public, depending on how the user has chosen to share them. If you are building an integration that requires access to private XD cloud ducments, your app will need an access token which can be obtained through an [OAuth integration](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/OAuth/OAuth.md).

During this OAuth workflow, users will be asked to authorize your app to access private cloud documents. 

|                       | API Key  | API Secret   | Access Token      |
|-----------------------|----------|--------------|-------------------|
| Public Cloud Docs     | Required | Not Required | Not Required      |
| Private Cloud Docs    | Required | Required     | Required          |


### 2. Get the document URL

You will need a document URL created from an XD document. In order to create a link, open Adobe XD and follow the steps below.

First, click on the "Share" button at the top right corner and select "Share for Review":

![Share for review](/images/share-button-click.png)

You will be asked to configure some settings. After choosing the right options for you, click on the "Create Link" button:

![Set options and create a link](/images/create-link-button-click.png)

After creating the link successfully, you will be able to copy the link to the clipboard:

![Copy link to the clipboard](/images/copy-link.png)

We'll use that link in the next step.


### 3. Find out what API endpoint can be used for a document URL

Send an `OPTIONS` call and read the response header to learn what API calls can be made for a particular XD document URL. Refer to the required headers and parameters in [the endpoint references page](/reference/index.md).

```
curl -I -X OPTIONS -H "x-api-key: YOUR-API-KEY" -H "X-AdobeXD-Link: https://xd.adobe.com/view/21652643-762a-41c6-5cd9-6342060e8aff-5754/" https://xdce.adobe.io/v2/api
```

This should return a response header like this:

```
Access-Control-Allow-Headers →Origin, Content-Type, Accept, X-Api-Key, X-AdobeXD-Link, User-Agent
Access-Control-Allow-Methods →OPTIONS
Access-Control-Allow-Origin →*
Access-Control-Expose-Headers →x-request-id, Content-Type, Content-Length, Link
Connection →keep-alive
Content-Length →0
Content-Type →application/json; charset=utf-8
Date →Mon, 14 Oct 2019 20:57:24 GMT
Link →</v2/document/21652643-762a-41c6-5cd9-6342060e8aff-5754>; rel=document
Server →openresty
Strict-Transport-Security →max-age=15552000; includeSubDomains
Vary →Accept-Encoding
X-Content-Type-Options →nosniff
X-DNS-Prefetch-Control →off
X-Download-Options →noopen
X-Frame-Options →SAMEORIGIN
X-Request-Id →gJeLsvCSjgTXhhDEp8uGMa0rnBrNeZXo
X-XSS-Protection →1; mode=block
```

The value of the `Link` key is the endpoint you can use to make further API calls. In this example, that value is:

```
/v2/document/21652643-762a-41c6-5cd9-6342060e8aff-5754
```


### 4. Make a `GET` call to the `document` endpoint

Now that you've retrieved the exact endpoint, you can make a `GET` call to the API. Refer to the required headers and parameters in [the endpoint references page](/reference/index.md).

```
curl -H "x-api-key: YOUR-API-KEY" https://xdce.adobe.io/v2/document/21652643-762a-41c6-5cd9-6342060e8aff-5754
```

This will return a JSON response that contains various data about the document, including the following and more:

- `id`
- `name`
- `thumbnail`
- `publisher`
- `artboardCount`
- `artboards`
- `homeArtboardId`
- `version`
- `lastupdated`
- `history`
- `assetID`
- `includesDevelopmentData`

You can leverage this response data in your integration as-is. Or, in some cases, you can use the data to dig deeper. We'll look how to do that with the `artboards` data in the next step.


### 4. Make a `GET` call to the `artboard` endpoint

The response we received above contains the `artboards` key with an array value of `artboard` objects. Each `artboard` object contains a unique `id`. You can use this value to make a `GET` call to the `artboard` endpoint. 

Note that you need to chain the artboard URL to the document URL used in the previous step. Refer to the required headers and parameters in [the endpoint references page](/reference/index.md).

```
curl -H "x-api-key: YOUR-API-KEY" https://xdce.adobe.io/v2/document/21652643-762a-41c6-5cd9-6342060e8aff-5754/artboard/5dec1809-bf44-4e9b-aef5-6e46e8aa18e9
```

This will return a response that contains various data about a given artboard, including:

- `id`
- `name`
- `resourceAPI`
- `thumbnail`
- `bounds`
- `viewportBounds`
- `triggers`
- `parent`

Congratulations on making your first couple of calls to the XD Cloud Content APIs!


## Next Steps

Now you're ready to move forward in building you integration with XD Cloud Content APIs.

- Browse the [endpoint references](/reference/)
- See working code in our [samples](/samples/index.md)