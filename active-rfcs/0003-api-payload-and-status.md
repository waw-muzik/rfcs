- Start Date: 2020-05-28
- Revision Date: 2021-01-15
- Target Major Version: 2.0
- Reference Issues: [#19](https://github.com/waw-muzik/rfcs/issues/19)

# Summary

Currently in our legacy API we don't manage the status codes, being 400, 200 and 500 the only errors that are returned. Specifically, clients that consume the API, when an error occurs, they do not get more information than a 500 status code. The idea is to add more verbosity to the API and that it correctly uses the status codes by adding verbosity and semantics to the responses.

# Basic example

```javascript
 if (!phone_number) {
    return response
      .status(200)
      .json({
        error: false,
        data: {
          type: 'users',
          id: 10,
          attributes: {
            user: 'test'
          }
        }
      });
  }
```
And with errors:

```javascript
 if (!phone_number) {
    return response
      .status(422)
      .json({
        error: true,
        errors: [
          {
            code: "PARAM_REQUIRED",
            status: "422",
            detail: "Phone number is required"
          }
        ]
      });
  }
```

# Motivation

By getting closer to the API Rest definition and using the HTTP status codes, we add more verbosity to our API, in addition to being able to know better, from the clients, what error has occurred in the request, so we can give better feedback to our users about what has happened, and what they can do.

# Detailed design

To add this new functionality, we need to review all the adonis services, so they always return status codes with an established payload.

We will use the status codes according to what is defined in [RFC7231](https://tools.ietf.org/html/rfc7231#section-6) and they will be grouped into:

* 1xx (Informational): The request was received, continuing process
* 2xx (Successful): The request was successfully received, understood, and accepted
* 3xx (Redirection): Further action needs to be taken in order to complete the request
* 4xx (Client Error): The request contains bad syntax or cannot be fulfilled
* 5xx (Server Error): The server failed to fulfill an apparently valid request

Payload for success responses:

```javascript
  return response
    .status(200)
    .json({
      error: false,
      data: {
        id: 569394,
        type: 'users',
        attributes: {
          user: 'test'
        }
        ...follow the structure that this endpoint need
      }
    });
```

Payload for a success response with a list of results:


```javascript
  return response
    .status(200)
    .json({
      error: false,
      data: [
        {
          id: 569394,
          type: 'users',
          attributes: {
            user: 'test'
          }
          ...follow the structure that this endpoint need
        },
        {
          id: 3247,
          type: 'users',
          attributes: {
            user: 'other'
          }
          ...follow the structure that this endpoint need
        }
      ]
    });
```

Payload for error responses

```javascript
  return response
    .status(422)
    .json({
      error: true,
      errors: [
        {
          code: "PARAM_REQUIRED",
          status: "422",
          detail: "Phone number is required"
        },
        {
          code: "RANDOM_ERROR",
          status: "422",
          detail: "More information related to this error"
        },
        {
          code: "ANOTHER_ERROR",
          status: "422",
          detail: "More information related to this error"
        }
      ]
    });
```

# Drawbacks

The problems that we can find when implementing these new status codes with this new payload, is when publishing the API and being consumed by our clients. This breaks all backward compatibility with customers who used our API, so we propose to make this change in a new major version.

# Alternatives

Although it has been considered to maintain the way in which our API works currently, this adaptation is the best since we would approach the defined standard for Restful services.

# Adoption strategy

We will add this update to a new major version following semver versioning, so all developers need to keep an eye on this, add it in our backend projects and adapt all exceptions and code to follow this package.

# Unresolved questions

The only management that does not remain is how we are going to manage the API versioning. This question will be resolved in another RFC.

# References

* Status Codes on IETF: https://tools.ietf.org/html/rfc7231#section-6
* HTTP Status Codes: https://httpstatuses.com/
* JSON API: https://jsonapi.org/format/#errors
  * Example JSON API: https://jsonapi.org/examples/#error-objects-error-codes