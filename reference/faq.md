# FAQ

Below you'll find answers to some frequently asked questions.

## What rate limits are there on API calls?

XD Cloud Content API integrations are limited to no more than 10 calls per second. 


## Do artboard thumbnails (renditions) have a lifespan?

Thumbnail URLs returned by the Cloud Content APIs are only live for 24 hours. Make sure that your application sends a new request to receive updated thumbnail URLs.


## Is it possible to access private XD cloud documents through these APIs?

Yes, provided that the user grants you [access via OAuth](../tutorials/quick-start.md#1-decide-whether-your-app-will-access-private-cloud-docs-or-not).

However, it is important to note that only private cloud documents created by **individual users** are accessible. Private cloud documents created by **enterprise users** will be supported in the future.

## What happens if I request a cloud document that has been deleted?

If the cloud document or its published link is deleted by the author, the API will return the following body in the response:

```
{
    "error": {
        "message": "Specified resource not found or not authorized"
    }
}
```