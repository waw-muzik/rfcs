<!--- NOTE
  * Remove sections that you don't need
  * Fill required sections, please, it's very improtant to share the knowledge about the RFC
-->
- Start Date: 2020-11-10
- Target Major Version: 2.0
- Reference Issues:
- Implementation PR:

<!--- ** Required Section ** -->
# Summary

In order to improve the quality of data in our API, we want to define a format to use dates. In our legacy API, we work with timestamps, dates following ISO-8607 and other formats ( like JS Date library format). Support multiple formats isn't good for an API and business logic, and for our clients will be hard to know the format and try to play and manage these dates. So de idea is to base all our dates on the same format, following ISO-8601 calendar system, such as 2007-12-03T10:15:30+01:00. Related to the timezone, the server will be always based on UTC Timezone, so the format should be always based on UTC+0 Timezone

<!--- ** Required Section ** -->
# Basic example

As we said, manage timezone it's hard and our server should only understand UTC+0 timezone, so our backend is agnostic to the timezone. This provides the power to our client to transform the data with Timezone it's they need it or not. So basically, our dates will be saved like this

Following ISO-8601 calendar system, such as:

For Dates: `2007-12-03`
For Time: `10:15:30`
For DateTime: `2007-12-03T10:15:30`

<!--- ** Required Section ** -->
# Motivation

In order to have an easy way to manage dates and work without timezone problems we want to use the most useful standard that related to dates. With this approach, we avoid timezone erros and support multiple date formats.

<!--- ** Required Section ** -->
# Detailed design

All details are included on the standard ISO-8601, but basically, this is the format to follow:

* Year:
  YYYY (eg 1997)
* Year and month:
  YYYY-MM (eg 1997-07)
* Complete date:
  YYYY-MM-DD (eg 1997-07-16)
* Complete format
  YYYY-MM-DDThh:mm:ss.sZ (eg 1997-07-16T19:20:30.45Z)

where:

```
  YYYY = four-digit year
  MM   = two-digit month (01=January, etc.)
  DD   = two-digit day of month (01 through 31)
  hh   = two digits of hour (00 through 23) (am/pm NOT allowed)
  mm   = two digits of minute (00 through 59)
  ss   = two digits of second (00 through 59)
  s    = one or more digits representing a decimal fraction of a second
  TZ   = time zone designator. Z for UTC+0
```

As we said, we don't want to use Timezone in our servers, because our servers will be on UTC format, so the timezone should be always UTC+0.

The full format should be like this `YYYY-MM-DDThh:mm:ss.sZ`, eg `1997-07-16T19:20:30.45Z`

<!--- ** Required Section ** -->
# Drawbacks

Clients (mobile or web) need to manage the timezone because on backend we will be based on UTC+0, so we will don't save timezones.

<!--- ** Required Section ** -->
# Alternatives

Another alternative could be use Unix Timestamp or Epoch time but after some research and considerations, we decide to use the ISO-8601 for some reasons, like follow the standard and because for developers, this format is more human-readable.

<!--- ** Required Section ** -->
# Adoption strategy

The idea is to use this standard in our new API because this will break backward compatibility.

# References

* ISO-8601: https://www.w3.org/TR/NOTE-datetime