---
layout: post
title: "Creating brand and notification sounds"
date: 2019-03-23 05:18:00 +0100
categories: [GAM720]
tags: [Diary, Project development]
---

In this post I've attempted to create synthesised sounds for both my logo, for use on the splash screen of Escape The App, and to notify users that a clue has been made available, for use during game play. I have to admit that I was a little daunted before undertaking this task as creating my own sounds is something I'd never done before, however my thinking was to approach this in the same way I would approach a visually creative task, which is to clarify the requirement and brainstorm solutions and see what happens as a consequence. Before I got into the creative part of the task I thought I would experiment a little with what's achievable so that I knew what I was working with and how to create sound in the first place.

### Experimenting with sound creation

I decided to experiment using [Audacity](https://www.audacityteam.org) as it's a program I am reasonably familiar with and I wanted to limit the steepness of my learning curve by not adding a new piece of software into the mix being that synthesised sound creation alone is a new concept to me and taking on the two together might be too much. I found this useful [video](https://www.youtube.com/watch?v=1ngGaYIzvsU) on YouTube that I coupled with some of the information on the [BBC Radiophonic Workshop Video](https://falmouthflexible.instructure.com/courses/296/pages/week-8-bbc-radiophonic-workshop?module_item_id=19103) to help me to understand how to start forming sound using tones. To summarise my experimentation I created six tones using a sine waveform with varying frequency and amplitude and experimented with what sounds could be achieved by soloing each track and editing the waveform using the envelope tool. Here's a grab of my tracks taken at some point during my experimentation:

![](/assets/img/GAM720_Wk8_Audacity--001.png)

I didn't need to play for long before I felt that I had enough to go back to the drawing board and brainstorm the type of sound I wanted for both my logo and my notification and then *attempt* to create these sounds using this technique in Audacity. At this point, if I am honest, I wasn't completely confident that I would create something production ready but I thought I'd give it a go regardless.

### Creating sound for my logo

For this sound I brainstormed the Escape The App brand and thought deeply about the story world I'm creating with my narrative. I journeyed through the idea of creating ominous and atmospheric dystopian sounds but decided in the end that I wanted to emphasise the feeling of urgency in my sound creation and experiment with the idea of having the timer sound I used in my game play experience alongside some tones to create a quick build to a beeping climax that then fades away ominously to nothing. So in just a few seconds I wanted to replicate the failure to escape a room using sound. Here's how I went about achieving this:

**Introducing the timer beeping**

I brought across five of the beeping sounds I'd used for my timer and laid these onto five tracks, each 200 milliseconds long and each one beginning directly after the other which (in total) spanned one second. I then tweaked the gain on each track so it grew by +0.5 DB for each beep to create the quick build I was looking for.

![](/assets/img/GAM720_Wk8_Audacity--002.png)

**Introducing the ominous fade out**

To create the ominous fade out I generated a new tone, this was a sine waveform with a frequency of 200, an amplitude at 0.64 and a duration of 3 seconds. This gave a dull tone. I then created another tone, again a sine waveform but this time with a frequency of 800 and an amplitude of 0.12. This gave a more high pitch tone. I then applied a fade out to both waveforms and edited them using the envelope tool to create a gradual rise in the sounds to peak at the end of the last beep.

![](/assets/img/GAM720_Wk8_Audacity--003.png)

**Introducing the climax**

I was encouraged by this point that the sound was beginning to take shape but I still felt that it lacked a high pitch climax. To create this I generated a new tone, again a sine waveform but this time with a higher frequency of 2400 and an amplitude of 0.64. This gave a high pitch beep similar to the imported beeping sound which is just what I was looking for. I then edited this with the envelope tool to create a sharp rise in the sound, I then edited the ominous tones to alter the gradual rise so it was more a sudden burst and after playing the sound over and over I concurred that I was pretty pleased with the result.

![](/assets/img/GAM720_Wk8_Audacity--004.png)

### Creating sound to notify users that a clue has been made available

Though I planned on brainstorming a variety of potential mimetic solutions for this sound, by the time I got to this point, having journeyed through synthesising the logo sound I had begun to form a pretty solid idea of how the synthesis for my notification should sound. It seemed quite clear that the notification sound I was searching for should be driven by the vessel which is used to deliver the sound. In my game play experience an intercom is used to deliver the narrative thus it seemed sensible to have one generic sound that I could use to identify that a new message is about to come over the intercom rather than having various bespoke sounds for certain events such as a clue being made available. The standout solution was to try and replicate the beep of a button being pressed followed by a static background noise that gives the impression that an audio feed that has been opened. From a programmatic point of view I would need two sounds to achieve this, one static sound to loop play behind the TTS message and then one single beep sound to simulate the button press. For the static sound it seemed more appropriate to use a stock sound or to record the sound myself, but having learned some basics of sound synthesis I could quite easily create the beep. I found this [stock example of an intercom beep](http://www.orangefreesounds.com/intercom-beep-sound) to use as reference. After listening closely to this I identified two parts to the sound; the first being the beep obviously and the second being the sudden attack of static behind this. Here's how I went about creating something similar to this:

**Creating the attacking background static**

To create the sudden attack of background static I generated some white noise with an amplitude of 0.8 and a duration of 1 second, I then editing the waveform using the envelope tool to create the sudden entry and gradual fade out to the sound.

![](/assets/img/GAM720_Wk8_Audacity--005.png)

**Creating the beep**

To create the beep I generated a tone with a sine waveform, a frequency of 1200 and an amplitude 0.64, I then edited the waveform using the envelope tool to match the sudden entry of the background static sound but in this case I gave the beep a sudden exit.   

![](/assets/img/GAM720_Wk8_Audacity--006.png)

This was sounding pretty close, but listening to the two sounds together helped me to identify that there was a third sound in the stock example that I'd missed before. Listening carefully to the example I could identify a click at the beginning of the sound so I set about adding this too.

**Creating the click**

At first I had no idea where to start with this and I did some quick research but that was quite unhelpful so I decided to have a play around in order to create the sound. I came to realise that a click can be created simply by creating a tone and then shortening it to have a sudden entry and exit. I generated a tone with a sine waveform and experimented with the frequency and eventually found that having a lower frequency of about 200 gave me a nice deep sound that when clipped using the envelope tool did sound much like the click I was after.

![](/assets/img/GAM720_Wk8_Audacity--007.png)

### Conclusion

Overall I'm pleased with the results of my experimentation into sound synthesis. As I stated at the beginning of this post, I was apprehensive about this task and quite honestly I didn't expect to create anything worth using in my app, so I'm relatively surprised that I have created something of merit and I had a lot of fun in the process. Of course, I am sure a sound expert would look at what I've done and say it sounds incredibly amateur, and I myself feel now listening to the logo sound again that it could be improved. However I feel that I've created a notification sound that I will use and I will set about adding this into my app soon. Here are the two complete sounds:

1. [Logo sound](/assets/sound/GAM720_Wk8_LogoSound.mp3)
2. [Intercom beep sound](/assets/sound/GAM720_Wk8_IntercomBeep.mp3)

Aside from creating sounds I will use in Escape The App, I am pleased that I've taken the time to try something new with this task. What I've learned in this post has definitely influenced me to approach sourcing sound differently than I would have before. I'm pleased with my timer sound that I created by combining stock sounds into a composition which is summarised in this [post]({% post_url 2019-03-16-week-7-experimenting-with-sounds %}), but in hindsight I realise I could quickly and easily have created that same sound using tones that I'd generated myself.

## Summary

In this post I've detailed my experiments with sound synthesis and creating sounds that I've concluded I will use in Escape The App. As a by-product of this experiment, I've also learned the makings of a new and valuable skill which will help to make me a better and more rounded creative application developer.

## References

1. [Audacity Sound Editor](https://www.audacityteam.org)
2. [Exploring Additive Synthesis Video on YouTube](https://www.youtube.com/watch?v=1ngGaYIzvsU)
3. [Intercom Beep Sound on Orange Free Sounds](http://www.orangefreesounds.com/intercom-beep-sound)
