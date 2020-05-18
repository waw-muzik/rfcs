- Start Date: (fill me in with today's date, 2020-05-22)
- Target Major Version: (1.0.0)
- Reference Issues: (fill in existing related issues, if any)
- Implementation PR: (leave this empty)

# Summary

Define how Waw Muzik will return any error from the API. The main purpose is to define a message structure with a message and an internal code, plus the HTTP code that acts in the action.

Use Twitter docs as an example: https://developer.twitter.com/en/docs/basics/response-codes

# Basic example

If the API returns a 404, give a more extensive info to our system (logs, apps, admin panel, partners) with a code and a message, like:

* WM0001 - User not found - HTTP 404
* WM0002 - Artist not found - HTTP 404


# Motivation

The main need is to have well documented any error/message returned by the API. Create a defined structure and a model for these error messages, gives the code consistency and makes easy the development job (and also error tracking).

With the HTTP code, the API clients will know what's going on and with the internal code, could have a detailed info of the given message.

# Detailed design

|HTTP Code|   |Internal code|   |Description|
|:---:|---|:---:|---|---|
|404|   |WM0001|   |Lorem ipsum lorem ipsum dolor sumun cafetasum|
|404|   |WM0002|   |Lorem ipsum lorem ipsum dolor sumun cafetasum|
|404|   |WM0003|   |Lorem ipsum lorem ipsum dolor sumun cafetasum|

# Adoption strategy

If we implement this proposal, every developer must refactor any API response to the new way and including the belonging info/internal code

# Unresolved questions

?
