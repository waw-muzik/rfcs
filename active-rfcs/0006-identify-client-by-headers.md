<<<<<<< HEAD
- Start Date: 2020-11-06
- Start Date: 2020-11-10
- Target Major Version: 2.0
- Reference Issues: *None*

# Summary

All clients may send a header in every request called "user-agent". This header must include the device type of SO or client that is calling the backend/API and also, the app version. This info will provide us some power tracing users bugs/problems/behaviors

# Basic example

We expect different user-agent by devide:
  * Android: android-com.wawmuzik.app-1.0.24-release
  * iOS: iOS-com.wawmuzik.app-1.0.6

# Motivation

When a user has a problem, without this info, we don't know exactly under which version is using the service neither the source (Android/iOS).

If we detect that some users have problem in the login/registration process, we would be able to debug the version afected or the backend if it is a general problem. Also, it adds some power if the bussiness team decides to create a marketing capaign targeting users.

The final motivation comes through the "force push" functionality. If we detect that some users are running under a very old app, we could need to alert he/she to update the app for any reason.

# Detailed design

The first step is to crea a middleware to be included in the requests to the API that you need. This middleware will be the responsible of saving the device and version in to the user info.

```js
  android-com.wawmuzik.app-1.0.24-release
  iOS-com.wawmuzik.app-1.0.6
```

The middleware has to process the given header and extract the device (android) and the app version (1.0.24).

Use a regular expresion to extract this numeric value:

```js
  const APP_VERSION = new RegExp(/\d+\.\d+\.\d+/, 'i');
```

# Drawbacks

*Nothing at this moment*

# Alternatives

*Not related*

# Adoption strategy

Mobile apps has included it on every call to the API. There isn't any problem if a client doesn't have, in this case the backend doesn't do any and the logged user won't have this info

# Unresolved questions

*Nothing at this moment*

# References

*Not related*
=======
<!--- NOTE
  * Remove sections that you don't need
  * Fill required sections, please, it's very improtant to share the knowledge about the RFC
-->
- Start Date: (fill me in with today's date, YYYY-MM-DD)  <!--- ** Required ** -->
- Target Major Version: (2.x / 3.x) <!--- ** Required ** -->
- Reference Issues: (fill in existing related issues, if any)
- Implementation PR: (leave this empty)

<!--- ** Required Section ** -->
# Summar

Brief explanation of the feature.

<!--- ** Required Section ** -->
# Basic example

If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable.

<!--- ** Required Section ** -->
# Motivation

Why are we doing this? What use cases does it support? What is the expected
outcome?

Please focus on explaining the motivation so that if this RFC is not accepted,
the motivation could be used to develop alternative solutions. In other words,
enumerate the constraints you are trying to solve without coupling them too
closely to the solution you have in mind.

<!--- ** Required Section ** -->
# Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with Vue to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

<!--- ** Required Section ** -->
# Drawbacks

Why should we *not* do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people Vue
- integration of this feature with other existing and planned features
- cost of migrating existing Vue applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

<!--- ** Required Section ** -->
# Alternatives

What other designs have been considered? What is the impact of not doing this?

<!--- ** Required Section ** -->
# Adoption strategy

If we implement this proposal, how will existing developers adopt it? Is
this a breaking change? How will this affect other WAW projects?

# Unresolved questions

Optional, but suggested for first drafts. What parts of the design are still TBD (to be determinated)?
>>>>>>> e8cbee4 (wip)
