---
title: Database Schema Ideas
---

P3: NASA Apollo Rich Audio Access
=================================

## Objective

Develop a schema to store Apollo data and meta-data.

## Background 

Previous attempts have captured at most 2 channels (air-to-ground and flight
director loops). Other loops were previously unavailable. Our recent
digitization efforts are going to make as many as 28 channels available. The
new schema should handle this.

## Merit/Impact

Simultaneous access to all audio channels will offer a new perspective on the
mission. Being able to selectively hear a subset of the channels will allow
investigators to follow conversation chains. Some of the critical features to
support will be the ability to move back and forth in time and channels (and
given the fact that the audio channels are going to be 10 days long).
Additionally, there will appreciation for a feature that allows user’s to play
multiple channels at the same time.

## Method

### List of data channels

#### Mission

*	Each mission can have its own ID
*	Mission Name (e.g., Apollo 11)
*	Mission Elapsed Time (this is measured from launch which is T=0). All metadata tends to be aligned with MET so this is very valuable field.
*	Missions Dates
*	Perhaps a description field
*	Each Mission will have its own (up to) 28 channels. 
*	Each Mission will have its own personnel (People can overlap between missions)

#### Controller Positions

*	Each controller position has its own audio Channels
*	Lets give each controller position its own DB ID
*	All mission controller positions have a name (e.g., Flight Director Loop, Air to Ground, FIDO, GUIDO, PAO, etc.). Here is a nice introduction (http://arstechnica.com/science/2012/10/apollo-flight-controller-101-every-console-explained/)
*	The mission controller position also has a specific role to perform.
*	Controller position were manned by personnel in overlapping shifts.

#### Mission Personnel

*	Lets give all mission personnel their own DB IDs
*	Name (e.g., Armstrong)
*	Position (e.g., Astronaut)
*	Assignment to a channel
*	Picture
*	Biography

#### Conversation

*	Multiple personnel participate in conversations on audio channels.
*	Many personnel can be present on one channel
*	In some cases conversations have been manually transcribed. In most cases, transcripts will be automatically generated using speech recognition.
*	In some cases, speaker diarization (who spoke what) has been done manually. In most cases, this will be done automatically.
*	If we think of of conversations as a series of overlapping dialogs. Then each dialog
  *	belongs to mission personnel
  *	has a transcript

### Additional Analysis

Additional analysis by algorithms will generate new (or automatically processed) meta-data. I am listing them here:
*	Word Count Analysis
*	Sentiment Analysis
*	Conversation Turn Taking Analysis

In general, we will tie these things up to MET. In this way, we will be able to
synchronize the analysis will audio channels. I would like to show these
analysis as add on widgets on our main audio access board.

Additional meta-data captured during the mission is also available:
*	Pictures
*	Videos 

These will also by synced with MET and can be displayed in separate widgets (lets discuss).

## Results

Pending. Populate post discussion.

## Conclusion

Pending. Populate post discussion.

## Appendix

![mission control][mission-control-img]

[mission-control-img]: assets/mission-control.png
