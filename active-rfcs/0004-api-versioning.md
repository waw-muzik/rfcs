- Start Date: 2020-05-28
- Revision Date: 2020-11-10
- Target Major Version: 2.0
- Reference Issues: *None*

# Summary

In order to improve our legacy API and code, we want to add or change some functionalities that may cause client versions that consume our API to stop working. To solve this problem and to add more functionalities without breaking anything, making the new clients (apps and websites) consume the new functionalities, we must add and manage different versions of our API.

# Basic example

```bash
curl -i -H " Accept: application/vnd.wawmuzik.v1+json" -H "Content-Type: application/json" http://app.wawmuzik.com/auth/login
```

and the API will send a response with this header:

```bash
Accept: application/vnd.wawmuzik.v1+json
```

# Motivation

We want to improve our API and business logic adding more semantic data, performance, how we use the database, ..., In order to avoid to break something, semantic versioning will be the best approach for this. For now, we will only use major versions, so all clients will be using something like v1, v2, v3 ...

# Detailed design

We will manage our API through semantic versioning, being the client who defines which version of the API they want to consume using this header

```bash
curl -i -H " Accept: application/vnd.wawmuzik.v1+json" -H "Content-Type: application/json" http://app.wawmuzik.com/auth/login
```

the response will come with this type of header:

```bash
Accept: application/vnd.wawmuzik.v1+json
```

In the backend, in our routers, we will need to check this header before doing anything in the endpoint. This will be managed by a Factory, which must be implemented soon.

For now, requests without this header will be redirected to the API's first version. This approach will be for now, for giving backward compatibility to the v1. When v1 becomes deprecated or gets removed, requests without this header will be redirected to the latest version

# Drawbacks

We will need to put time to do this and test that this works well. We need to add versioning, but we need to be sure that we don't break the previous versions that our clients are using.

# Alternatives

We considered to use API versioning in different ways, for example:

* Use version in path, like this `/api/v1/auth/me`: the problem with this os that we will need to rewrite the whole api to use this new endpoint, and we will break hyper medias in our clients.

* Custom header, like `X-version: 1.0`: This will be good too, but the accept and content-type work
Thinking in a future, using versioning in a header will be good to work with micro-services

# Adoption strategy

This is a breaking change so it will be available since version 2 of the API, and all the clients need to use it since we publish it.

# Unresolved questions

How will we update the old clients and inform them that they need to update the apps? With push notifications? SMS? ...

# References

* APIS you wont hate: https://apisyouwonthate.com/blog/api-versioning-has-no-right-way
* FreeCodeCamp: https://www.freecodecamp.org/news/how-to-version-a-rest-api/
* Restful API: https://restfulapi.net/versioning/