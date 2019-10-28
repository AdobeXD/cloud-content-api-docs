# Go Live

If you are ready to go live with your integration, makes sure to read the following sections.


## Rate limits

Your integration is prohibited from making more than 100 calls per second. This rule applies to all of your integrations with any Adobe APIs. If you have a use case that needs this restriction to be lifted, please contact us. 

## Thumbnail lifespan

Note that links to thumbnails returned by the APIs are only live for 24 hours. Make sure that your application sends a new request to received the updated links.

## Private cloud doucment access

Note that only prviate cloud ducuments created by individuals are accessible through these APIs. Private cloud ducuments created by enterprises will be supported in the future.

## Deleted cloud document

If the cloud document or its published link is deleted by the author, the API will return the following body in the response:

```
{
    "error": {
        "message": "Specified resource not found or not authorized"
    }
}
```