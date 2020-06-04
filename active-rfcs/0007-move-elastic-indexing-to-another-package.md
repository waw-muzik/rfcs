<!--- NOTE
  * Remove sections that you don't need
  * Fill required sections, please, it's very improtant to share the knowledge about the RFC
-->
- Start Date: 2020-06-04  <!--- ** Required ** -->
- Target Major 1.0 <!--- ** Required ** -->
- Reference Issues:
- Implementation PR:

<!--- ** Required Section ** -->
# Summary

Currently, the process of reindexing in Elastic is done from the backend project itself, and also, it is done using HTTP requests, which is not very usable, and also the request responds with a timeout since our database grows exponentially with the songs and catalogs.

The idea will be move this process to an stand-alone package that manage all this type of things, and that we can add as devDependency in all projects that we need to index something in Elastic.

<!--- ** Required Section ** -->
# Basic example

The idea is to make a new project calles `Elastico` that manage this type of things. This project need to publish a bin script that we can run in all our projects and use a shared config that we will define in our projects.

<!--- ** Required Section ** -->
# Motivation

Use HTTP to reindex is a bad decision because we get a lot of timeouts and it's not the most secure way to do this type of things. This type of script and actions must be used by a script that runs in the server because we want to work with a big amount of data.

Thinking in the future, this will be a good approach, because we will reuse this script with the new API and another side projects that we will run and need to do something with Elastic.

<!--- ** Required Section ** -->
# Detailed design

* This package will be installed in different projects (as backend project, for example)
* Need to export a bin script, so we can use it in backend project or another project.
* Need to provide a way to index things in Elastic, to use in the project when we add/update/remove something from the database.
* Must define a config file `.elasticorc` when we will put the elastic mapping and database connection, ... Something like this, for exmaple

```
/.elasticorc
{
  database: { ... },
  elastic: {
    {
      song: {
        name: { type: 'text' }
      },
      user: {
        username: { type: 'text' }
      },
      album: {
        name: { type: 'text' }
      },
      artist: {
        name: { type: 'text' }
      },
      genre: {
        name: { type: 'text' }
      },
      playlist: {
        name: { type: 'text' },
        status: { type: boolean, index: false }
      },
      article: {
        title: { type: 'text' }
      },
      sponsor: {
        name: { type: 'text' }
      }
    }
  }
}
```

<!--- ** Required Section ** -->
# Drawbacks

The cost of the implementations will be high, but the benefits are clean, it's a most and effective way to do these type of jobs.

<!--- ** Required Section ** -->
# Alternatives

The other option will be using the same way that we use right now, but, for the new API, we will need to remake the code in this new project, and continue using an HTTP request. In the future, when we will move to microservices, all microservices will use this package, and index things that they need.

<!--- ** Required Section ** -->
# Adoption strategy

Working as a stand-alone package, the first thing will be playing with it. If it works, we will add in the backend project to use for reIndex, at the beginning. Later, we will use it to index when we add/update or remove some data. After this, we will remove the current code and remove the dependency from Adonis.
