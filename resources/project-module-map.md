---
title: Project Module Map
---

## Project Overview
The goal of this project is to build an interface that makes the 14,000 hours of Apollo Mission audio discoverable. Filtering, searching, and visualization of the audio should be possible. The goal of this thread is to organize the engineering effort for the critical path. 

## Project Modules 
For simplicity, I'm going to refer to the end-user accessible domain as "domain.com". Note that the implementation details are suggestions at this point. More research is needed to confirm these suggestions. 


![apollo project overview](https://cloud.githubusercontent.com/assets/2192970/9727095/aff5378a-55c0-11e5-8f5c-61b2a88686fb.png)

![apollo project overview2](https://cloud.githubusercontent.com/assets/2192970/9727098/b264e9ca-55c0-11e5-9b98-4e1f848a6e6c.png)


### P500: Static Informational Website
The static website is the entry point for the application. When you go to "domain.com" it will load a static landing page. This landing page is a part of a static website that contains pages such as an about page, a team page, and blog posts. This static website has a call-to-action that links to P100, the single page application. We will host the single page application separately on a separate domain. 

####  Implementation Details
This static website is built using Jekyll, a static site generator. 

#### Infrastructure
The website is deployed and hosted via GitHub pages.

### P100: Single Page Application
This rich JavaScript application that provides the interface for the data. We still need to confirm the exact features. However, let's start with the most important vertical slice: be able to play the mission audio and filter the channels that make up the audio stream. 

#### Implementation Details
We will use React to handle the view layer. Virtual DOM diffing is the state of the art. The react ecosystem and the tooling are very mature at this point. Component-driven development has serious advantages:
* The components have no knowledge of where the data used in a particular component originates. As such, an application can be prototyped without a completed backend.
* React components render deterministically, so testing and prototyping is easy.
* Components are easy to reason about and force good project structure. 

I recommend [redux][], a [flux][] implementation, for maintaining the application state. Redux opens the door to some seriously slick development workflows. I highly recommend [checking it out.](http://youtu.be/xsSnOQynTHs). It's a match made in heaven for applications like ours where we are receiving and responding to continuous events from the server.

We are going to write our code in ES6/7 and have it transpiled to ES5 using [babel][]. [Webpack][] will serve as our module loader and build tool. 

#### Infrastructure 
This project will compile down to a set of static files. The static files will live on AWS S3. We will stick AWS Cloudfront or Cloudflare in front of the S3 bucket as a CDN. This setup will infinitely scale to any number of users and is extremely performant. 

### P200: API Server
This module provides an API for the data that drives the front-end application. It exposes REST endpoints and possibly a WebSocket endpoint if needed. It composes all of the other server-side modules behind the scenes into responses the single-page app can consume. 

We implement features like user authentication and search here. 

#### Implementation Details
Probably a Node app, perhaps using the Express web framework. In my experience, Node is very productive and has a rich package ecosystem. It seems that everybody in the group has at least *some* JavaScript experience, so I feel everyone can chip in here. 

#### Infrastructure 
Deploy to Heroku and be done with it. 

### P300: Audio Control Server
A Webservice that returns a customized stream of audio based on request parameters. It grabs the requested audio track files, syncs them up, mixes the audio together, and streams it to the browser. 

#### Getting Help
I have a connection to some engineers at Pandora. I feel like they could give us some really good pointers as to how to handle on-demand audio mixing and such. if you guys have any resources, let me know. 

#### Implementation Details
I am not completely sure what language we will implement this in yet. My vote is for Go. Go is good at stuff like this. It looks like there are libraries out there for mixing audio. Also, since it compiles down to a binary, it is easy to manage a bunch of clustered app servers. Python might be another interesting option. I don't even have to look to know there is probably an extremely good audio processing library available. 

##### Workers
The audio control server has a web process that handles and parses requests. Since these requests are long-running, work-intensive, concurrent, and stateful, we should be delegating the request handling to workers. Workers should be discrete machines that perhaps have a maximum amount of concurrent requests they can service. The worker pool should be able to grow dynamically and shrink based on the amount of requests that need to be satisfied. 

##### Formats
It would not be web development if we did not have to mess with stupid browser stuff. Chrome and Safari are OK with MP3 files. Firefox needs Ogg Vorbis though. So we either need to handle transcoding in the mixer, or we need to stick a transcoding service in front of this module. 

##### Caching 
Mixing audio on the fly is obviously expensive. We should investigate some long-term caching. Theoretically if our users have listened to all the possible combinations of the channels end-to-end, we should not be doing any audio processing and should just be reading from the disk. 

#### Infrastructure
We could probably prototype this on Heroku. The problem with Heroku in the long-run will be getting compute optimized boxes. Compute-optimized boxes on Heroku are very expensive. Wherever we host this, it needs to support clustering and easy worker management. 

One choice that is interesting is AWS Lambda. Each audio request could get its own personal container. Theoretically Lambda infinitely scales since each listener would have a server that is spun up solely to meet their request. 

### P400: Database Server and Track Storage
The database that contains the metadata and the URLs to the audio objects stored on s3. 

#### Implementation Details
The database is Postgres. It has tables for metadata and audio tracks. Audio tracks live in s3. Maybe we have to break the tracks into smaller chunks. 

#### Infrastructure
The database should live on AWS RDS. We should take advantage of the robust snapshotting and backup capabilities RDS offers. 

[flux]: http://facebook.github.io/flux/docs/overview.html#content
[redux]: http://rackt.github.io/redux/index.html
[webpack]: http://webpack.github.io
[babel]: https://babeljs.io
