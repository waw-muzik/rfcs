# RFCs
RFCs or technology decision making

# What’s an RFC?

The name itself is a reference to the IETF’s Request For Comments process, and basically involves a document or series of documents which are drafted, reviewed, and eventually ratified (approved) by the WAW Muzik Team through discussion among those interested.

An RFC can extend, modify, or alter any part of the WAW Muzik technical decisions, whether or not it’s been documented. This includes the Code of Conduct, the Enforcement process, and anything else that affects a significant part of the engineering team. It can also propose entirely new policies and community agreements.

# The RFC life-cycle
An RFC goes through the following stages:

* __Preparing__: when the RFC is submitted as a draft PR. All people can see this proposal but it's not open to comments (for now) and the author is improving the description before send it.
* __Pending__: when the RFC is submitted as a PR and it's open to any comments or improvements
* __Active__: when an RFC PR is merged and undergoing implementation.

# How do I create an RFC?

* Fork https://github.com/waw-muzik/rfcs/
* Copy 0000-template.md into [NUMBER]-your-rfc-name.md
* Fill in and edit the template with your proposal
* Submit a PR to the npm/rfcs repo

# Implementing an RFC
The author of an RFC is not obligated to implement it. Of course, the RFC author (like any other developer) is welcome to post an implementation for review after the RFC has been accepted.

An active RFC should have the link to the implementation PR listed if there is one. Feedback to the actual implementation should be conducted in the implementation PR instead of the original RFC PR.

If you are interested in working on the implementation for an 'active' RFC, but cannot determine if someone else is already working on it, feel free to ask (e.g. by leaving a comment on the associated issue).