# Errors

<aside class=error>
This error section is stored in a separate file in `includes/_errors.md`. Slate allows you to optionally separate out your docs into many files...just save them to the `includes` folder and add them to the top of your `index.md`'s front matter. Files are included in the order listed.
</aside>

The SkyPAth API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- The request could not be understood by the server due to malformed syntax.
401 | Unauthorized -- Your API key or JWT token is wrong or expired.
403 | Forbidden -- You have the right token but unauthorized to execute the operation.
404 | Not Found -- The specified info could not be found.
405 | Method Not Allowed -- You tried to access a function with an invalid method.
406 | Not Acceptable -- You requested a format that isn't JSON.
410 | Gone -- The data requested has been removed from our servers.
418 | I'm a teapot :-)
429 | Too Many Requests -- You're requesting too much data! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
