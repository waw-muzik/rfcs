- Start Date:2020-05-20
- Target Major Version: 2.0.0
- Reference Issues:
- Implementation PR:

# Summary

We want to use the same error tracker and exception manager in all of our microservices so will be very useful to manage it in the same way.

# Basic example

```
const err = new WAWException({
  code: 'LOGIN_ERROR',
  message: 'There is an error trying to do login',
  error: {
    stack: err.stack,
    message: err.message
  },
  additionalData: moreData
});

err.track();

throw err;
```

# Motivation

Managing all the exceptions as we want in a generic way, in addition to tracking the errors in the error tracker that we want (Sentry, Loggly, ...)

# Detailed design

Create a npm package called `@waw/exceptions` that export 3 methods

```
export { WAWException, init, follow }
```

The first thing, will by init the exception manager, like this

```
init({
  apikey: ...,
  env: ...,
});
```

we can add the user data to, if we want to add some information related to the auth and user that generate this exception

```
follow({
  id: auth.user.id,
  email: auth.user.email,
  username: auth.user.username
});
```

and create and track the exception that we want

```
const err = new WAWException({
  code: 'LOGGIN_ERROR',
  message: 'There is an error trying to do login',
  error: {
    stack: err.stack,
    message: err.message
  },
  additionalData: moreData
});

err.track();

throw err;
`
```

# Adoption strategy

We will add semver versioning fot his package, so all developrs need to keep an eye on this, add it in our backend projects and adapt all exepctions and code to follow this package.