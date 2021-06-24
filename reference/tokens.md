# Endpoint References
The below security checklist is a general guidance to all integrations using Adobe IMS authorization to access private XD artefacts. There could be other security requirements for your integration depending upon your design.  

#### Security Checklist
##### Security Checklist:

Security Checklist


##### Client Side

|   | Client Side                                                            |   | Server Side |
| - | ---------------------------------------------------------------------- | - | ------------------------------------------------------------------------------------------------ |
|   | Use state parameter to prevent CSRF attack                             |   | Perform Online token validation                                                                  |
|   | Do not pass tokens in query string                                     |   | Pass ‘type’ parameter for validate token API                                                     |
|   | Avoid storing access token and user profile in browser’s local storage |   | Do not log IMS tokens in logs                                                                    |
|   | Ensure tokens are sent over TLS (HTTPS)                                |   | Never include your IMS client secret and permanent auth code in source code; Store them in Vault |
|   | Use latest version of IMS APIs                                         |   | Check for ‘system’ scope before providing access to a resource in service to service calls       |
|   |                                                                        |   | Encrypt refresh/access token while storing them on the server side                               |
|   |                                                                        |   | Check if access token belongs to your application or client                                      |


##### Server Side

|   | Client Side                                                            |   | Server Side |
| - | ---------------------------------------------------------------------- | - | ------------------------------------------------------------------------------------------------ |
|   | Use state parameter to prevent CSRF attack                             |   | Perform Online token validation                                                                  |
|   | Do not pass tokens in query string                                     |   | Pass ‘type’ parameter for validate token API                                                     |
|   | Avoid storing access token and user profile in browser’s local storage |   | Do not log IMS tokens in logs                                                                    |
|   | Ensure tokens are sent over TLS (HTTPS)                                |   | Never include your IMS client secret and permanent auth code in source code; Store them in Vault |
|   | Use latest version of IMS APIs                                         |   | Check for ‘system’ scope before providing access to a resource in service to service calls       |
|   |                                                                        |   | Encrypt refresh/access token while storing them on the server side                               |
|   |                                                                        |   | Check if access token belongs to your application or client                                      |


##### Logging

* If you need to log IMS tokens for debugging purpose then you should remove the signature part from the token which makes it invalid. The token format is HEADER.PAYLOAD.SIGNATURE.  Alternatively, you could log the decoded JSON payload which is search friendly.
* Keep in mind access token might contain PII data. Talk to Legal/ASSET researcher to come up with the right strategy. 


##### Client side token storage

Avoid storing IMS user access token in browser cookie. Use browser's session storage to persist any sensitive data. If you are using IMS javascript library then the access token and profile information will already be stored in session storage for you. 
If you are storing IMS access token in cookie and using it as session cookie then you need to make sure to
* Implement CSRF protection 
* Set 'Secure' flag to the cookie. This instructs the browser to send the cookie information only over HTTPS.
* Set 'HTTPOnly' flag if you are setting the cookie using server side code. 


##### Server side token storage

Application might have to store access token or refresh token on the server side for certain use case or while using refresh token grant type. Refresh token and access token must be kept confidential in transit and storage. The token should to be encrypted by the application and stored in the database. (Do not use disk level encryption or transparent data encryption as they don't protect the tokens against SQL injection type attacks). 



##### Secret Storage
* If you have IMS credentials in source code or accidentally committed them in your source code repository then you need to reach out to IMS team to rotate the credentials. 
* Make sure to store the new credentials in Adobe's approved secret storage system. 
* Rotation policy: General guidelines is to rotate the credential if it is leaked or person who had access to the credential left Adobe/team. 






#### GET
##### Summary:

Document API to get latest version of link identified by {linkID}

##### Description:

fetch manifest of link identified by {linkID}


##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| linkID | path | pass an ID to fetch a particular link's manifest | Yes | string |
| version | query | version of spec to be fetched | No | string |
| Accept | header | media type and schema version. Please use the fully qualified Accept header like in example for consistent response. If the schema version is not present, the latest version of the response will be returned | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Specified resource not found or not authorised / Wrong or missing authorisation |
| 404 | Specified resource not found |
| 500 | internal server error |
| 504 | Cannot connect to data normalizer / Cannot connect to Link Services / Cannot connect to Storage Services / Cannot connect to Community Platform |

### /v2/document/{linkID}/artboard/{artboardID}

#### GET
##### Summary:

get artboard identified by {artboardID} from link identified by {linkID}

##### Description:

fetch an artboard identified by {artboardID} from link identified by {linkID}

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| linkID | path | pass an ID to fetch a particular link's data | Yes | string |
| artboardID | path | pass an ID to fetch a particular artboard of the link | Yes | string |
| version | query | version of primary resource from where the artboard has to be fetched | No | string |
| Accept | header | media type and schema version. Please use the fully qualified Accept header like in example for consistent response. If the schema version is not present, the latest version of the response will be returned | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Specified resource not found or not authorised / Wrong or missing authorisation |
| 404 | Specified resource not found |
| 500 | internal server error |
| 504 | Cannot connect to data normalizer / Cannot connect to Link Services / Cannot connect to Storage Services / Cannot connect to Community Platform |