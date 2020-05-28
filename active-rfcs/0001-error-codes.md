- Start Date: 2020-05-18
- Target Major Version: 2.0.0
- Reference Issues:
- Implementation PR:

# Summary

Define how Waw Muzik will return any error from the API. The main purpose is to define a message structure with a message and an internal code, plus the HTTP code that acts in the action.

Use Twitter docs as an example: https://developer.twitter.com/en/docs/basics/response-codes

# Basic example

If the API returns a 404, give more extensive info to our system (logs, apps, admin panel, partners) with a code and a message, like:

* WM0001 - User not found - HTTP 404
* WM0002 - Artist not found - HTTP 404


# Motivation

The main need is to have well documented every error/message returned by the API. Creating a defined structure and a model for these error messages, gives the code consistency and makes the development job easy (and also error tracking).

With the HTTP code, the API clients will know what's going on and with the internal code, will have detailed info of the given message.

# Detailed design

|HTTP Code|   |Internal code|   |Description|
|:---:|---|:---:|---|---|
|404|   |WM0001|   |Lorem ipsum lorem ipsum dolor sumun cafetasum|
|404|   |WM0002|   |Lorem ipsum lorem ipsum dolor sumun cafetasum|
|404|   |WM0003|   |Lorem ipsum lorem ipsum dolor sumun cafetasum|

# Adoption strategy

If we implement this proposal, every developer will have to refactor every API response to the new way and include the belonging info/internal code
