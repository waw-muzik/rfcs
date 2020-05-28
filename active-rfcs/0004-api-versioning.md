- Start Date: 2020-05-28
- Target Major Version: 2.0.0
- Reference Issues:
- Implementation PR:

# Summary

In order to improve our legacy API and code, we want to add or change some functionality that may cause client versions that consume our API to stop working. To solve this problem and add more functionalities without breaking anything, making the new clients (apps and websites) consume the new functionalities, we must add and manage different versions of our API.


# Basic example

```bash
curl -i -H " Accept: application/vnd.wawmuzik.v1+json" -H "Content-Type: application/json" http://app.wawmuzik.com/auth/login
```

and the API will send a response with this header:

```bash
Content-Type: application/vnd.wawmuzik.v1+json
```

# Motivation

We want to improve our API and business logic adding more semantic data and improving a lot of things, for no break anything semantic versioning will the best approach for this. For now, we will only mayor versions, so all clients will be using something like v1, v2, v3 ...

# Detailed design

We will manage our API through semantic versioning, being the client who defines which version of the API they want to consume using this header

```bash
curl -i -H " Accept: application/vnd.wawmuzik.v1+json" -H "Content-Type: application/json" http://app.wawmuzik.com/auth/login
```

the response will be come with this type of header:

```bash
Content-Type: application/vnd.wawmuzik.v1+json
```

In backend, in our routers, we will need to check this header before do something in the ednpoint, so we will need to make a Factory that manage this behaviour.

For now, requests that don't have this header will be redirected to the first version of our API. This approach will be for now, because in the future, when we will remove this 1 version, requests that don't have this header, will be redirected to the latest version


# Drawbacks

We will need to put time to do this and test that this works well. We need to add versioning, but we need to be sure that we don't break the previous versions that our clients are using.

# Alternatives

We considered to use API versioning in a different way, for example:

* Use version in path, like this `/api/v1/auth/me`: the problem with this comes that we will need to rewrite the whole api to use this new endpoint, and we will break hyper medias in our clients.

* Custom header, like `X-version: 1.0`: This will be good too, but the accept and content-type work
Thinking in a future, use versioning in a header will be good to work with micro-services

# Adoption strategy

This is a breaking change so will be available since version 2 of the API, and all clients need to be use it since we publish it.

# Unresolved questions

How we will update the old clients and inform them that they need to update the apps? With push notifications? SMS? ...
