- Start Date: 2020-11-06
- Target Major Version: 1.22.1
- Reference Issues: (fill in existing related issues, if any)
- Implementation PR: (leave this empty)


# Summary

All clients may send a header in every request called "user-agent". This header
must include the device type of SO or client that is calling the backend/API and also, 
the app version. This info will provide us some power tracing users bugs/problems/behaviors


# Basic example

For an Android call: android-com.wawmuzik.app-1.0.24-release


# Motivation

When a user has a problem, without this info, we don't know exactly under which version is using
the service neither the source (Android/iOS).

If we detect that some users have problem in the login/registration process, we would be able to
debug the version afected or the backend if it is a general problem. Also, it adds some power if 
the bussiness team decides to create a marketing capaign targeting users.

The final motivation comes through the "force push" functionality. If we detect that some users 
are running under a very old app, we could need to alert he/she to update the app for any reason.

<!--- ** Required Section ** -->
# Detailed design

The first step is to crea a middleware to be included in the requests to the API that you need. 
This middleware will be the responsible of saving the device and version in to the user info.

```js
android-com.wawmuzik.app-1.0.24-release
```

The middleware has to process the given header and extract the device (android) and the app version (1.0.24).

Use a regular expresion to extract this numeric value:
```js
const APP_VERSION = new RegExp(/\d+\.\d+\.\d+/, 'i');
````

<!--- ** Required Section ** -->
# Adoption strategy

Mobile apps has included it on every call to the API. There isn't any problem if a client doesn't have, 
in this case the backend doesn't do any and the logged user won't have this info
