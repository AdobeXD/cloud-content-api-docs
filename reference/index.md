# Endpoint References
GET API's to discover and fetch published specs and prototypes the client can access

### /v2/api

#### OPTIONS
##### Summary:

Discovery API to get Cloud Content API entry point for given publish link

##### Description:

discovery API for a given published URL as header parameter


##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| X-AdobeXD-Link | header | published XD artefact link to discover corresponding Cloud Content API endpoint | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 403 | Api key is invalid |
| 422 | X-AdobeXD-Link in request header has missing/invalid published URL |

### /v2/document/{linkID}

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