---
layout: post
title: Spring 2016 Project Update
---

# Overall Summary

We were able to complete development on the first iteration of the platform. This includes a fully functional slice of the application that includes:

- Audio server that streams requested audio slices
- API Server with backing database schema to represent the models used in our application
- Front-end that fully supports all of the functionality of the API server.

We now have a fully functioning, production ready web application that features Missions, Stories, Moments.

# Work Summary

The following action items were completed:

- Audio server constructs and streams arbitrary audio based input
- Enhance the database schema to accommodate application data
- Build API server
- Build Data Loading API
- Complete Browser Application
- Comprehensive deployment strategy
- Comprehensive test strategy

## Audio Server

Last semester we had a proof of concept audio server that would do the job of
taking clips of audio, merging them together, and streaming them to the
browser. This semester we completed this functionality by building a fully
functioning web service around the proof of concept.

The audio server now takes arbitrary input parameters, consults the database,
and builds a audio clip for a moment. This is a critical piece of the
application, as all the audio played in the app originates from this server.

## Enhance Database Schema

Last semester we had a basic database schema ready to go. We have since created a fully production ready database schema that can handle all the data needed to support the application. We have also implemented database management procedures to facilitate further changes to the db structure.

At the time of writing this is what the database schema looks like: https://github.com/UTD-CRSS/exploreapollo-api/blob/a2c6692044afb9c3a6f03d50872b8b9a37c7f083/db/erd.pdf

## Build API Server

Last semester we had a proof of concept API server written in node.js. We have
since created a fully production ready API server built on ruby on rails.  Ruby
on Rails is a well respected and well documented web application framework.
This makes it easy to make changes in the future.

We implemented all the business logic for Missions, Stories, Moments as well as
made accommodations for metrics. The API server also provides a layer of
abstraction for the audio server. The API server talks to the audio server and
caches the responses for performance reasons.

## Data Loading API

We created an automated interface for loading data into the system.
Instructions are viewable here:
https://github.com/UTD-CRSS/exploreapollo-api/wiki/Backend-API

This is important because it allows someone to mass-import data such as
stories, moments, audio clips, photos using a script.

## Browser Application

We made significant improvements to the browser application. 

### Home Page

[https://app.exploreapollo.org/]()

### Mission Viewer

[https://app.exploreapollo.org/stories?mission=apollo11]()

### Story Viewer

[https://app.exploreapollo.org/stories/story/1]()

Stories now have a playlist mode that links moments together.

### Moment Viewer

[https://app.exploreapollo.org/stories/story/1/moment/1]()

The moment viewer now has a waveform added to the audio player. The transcripts are also highlighted live as the audio plays. We added support for pictures and graphs.

## Comprehensive Deployment Strategy

We created a deployment strategy that allows one to make a change to the code and promote the change all the way from a testing environment to a staging environment and finally to production.

This is needed to avoid interruptions and bugs making their way to production. Otherwise active users could be disturbed by our changes.

## Comprehensive Testing Strategy

The browser application has a fully automated testing suite. This is important to catch regressions in the various versions of browsers users will use the application with.

We set up the framework for tests on the API server but largely did not implement them.
