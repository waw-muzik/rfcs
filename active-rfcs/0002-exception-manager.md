- Start Date:2020-05-20
- Revision Date: 2020-11-10
- Target Major Version: 2.0
- Reference Issues: *None*

# Summary

We want to use the same error tracker and exception manager in all of our microservices so if will be very useful to manage it in the same way.

# Basic example

```js
const err = new WAWException({
  code: 'LOGIN_ERROR',
  info: [
    {
      title: 'info field 1',
      data: Object
    },
    {
      title: 'info field 2',
      data: Object2
    }
  ],
  userData: {
    id: user.id,
    email: user.email,
    username: user.username
  },
  tags: [
    {
      key: 'key 1',
      value: 'value 1'
    }
  ],
  exception,
  severity,
  headers
});

err.track();

throw err;
```

# Motivation

Managing all the exceptions as we want in a generic way, in addition to tracking the errors in the error tracker that we want (Sentry, Loggly, ...)

# Detailed design

Create a npm package called `@waw/exceptions` that exports 3 methods

```js
export { WAWException, init, follow }
```

The first thing, will be creating the exception running the `init` method of the exception manager, like this

```js
init({
  apikey: ...,
  env: ...,
});
```

we can add the user data too, if we want to add some information related to the auth and user that generates this exception

```js
follow({
  id: auth.user.id,
  email: auth.user.email,
  username: auth.user.username
});
```

and create and track the exception that we want

```js
const err = new WAWException({
  code: 'LOGIN_ERROR',
  info: [
    {
      title: 'info field 1',
      data: Object
    },
    {
      title: 'info field 2',
      data: Object2
    }
  ],
  userData: {
    id: user.id,
    email: user.email,
    username: user.username
  },
  tags: [
    {
      key: 'key 1',
      value: 'value 1'
    }
  ],
  exception,
  severity,
  headers
});

err.track();

throw err;

```

# Drawbacks

*Nothing at this moment*

# Alternatives

*Not related*

# Adoption strategy

We will add semantic versioning for this package, so all developers need to keep an eye on this, add it in our backend projects and adapt all the exceptions and code to follow this package.

# Unresolved questions

*Nothing at this moment*

# References

*Not related*