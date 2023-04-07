# Errors

The lukaz API uses the following error codes:

Error Code | Meaning
---------- | -------
400        | Bad Request -- The request could not be understood by the server due to malformed syntax.
401        | Unauthorized -- Your API key is wrong.
402        | Unauthorized -- Subscription quota exceeded.
403        | Forbidden -- You don't have access to the requested resource.
404        | Not Found -- The specified resource could not be found.
405        | Method Not Allowed -- You tried to access a resource with an invalid method.
429        | Too Many Requests -- You're requesting too many resources at the same time.
500        | Internal Server Error -- We had a problem with our server.
503        | Service Unavailable -- We're temporarily offline for maintenance.
