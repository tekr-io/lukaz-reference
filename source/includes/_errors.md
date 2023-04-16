# Errors

The lukaz API uses the following error codes:

Code       | Meaning
---------- | -------
400        | Bad Request - Request has malformed syntax.
401        | Unauthorized - Your API key is wrong.
402        | Unauthorized - Subscription quota exceeded.
403        | Forbidden - You don't have access to the resource.
404        | Not Found - The specified resource could not be found.
405        | Method Not Allowed - Request has an invalid method.
415        | Unsupported Media Type - The file extension is not supported.
429        | Too Many Requests - Too many requests at the same time.
500        | Internal Server Error - We had a problem with our server.
503        | Service Unavailable - We're temporarily offline for maintenance.
