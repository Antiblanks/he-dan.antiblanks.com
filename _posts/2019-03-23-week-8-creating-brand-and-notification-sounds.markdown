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

??

### Conclusion

Overall I'm pleased with the results of my experimentation into sound synthesis. As I stated at the beginning of this post, I was apprehensive about this task and quite honestly I didn't expect to create anything worth using in my app, so I'm relatively surprised that I have created something of merit. Of course, I am sure a sound expert would look at what I've done and say it sounds incredibly amateur, and I'm sure I myself will revisit this task again to improve on the sounds I've created, but for now I think I have created sounds I will use and I will set about adding these into my app soon.

Aside from creating sounds I will use in Escape The App, I am pleased that I've taken the time to try something new with this task. What I've learned in this post has definitely influenced me to approach sourcing sound differently than I would have before. I'm pleased with my timer sound that I created by combining stock sounds into a composition which is summarised in this [post]({% post_url 2019-03-16-week-7-experimenting-with-sounds %}), but in hindsight I realise I could easily have created that same sound using tones that I'd generated myself.

## Summary

In this post I've detailed my experiments with sound synthesis and creating sounds that I've concluded I will use in Escape The App. As a by-product of this experiment, I've also learned the beginnings of a new and valuable skill which will help to make me a better and more rounded creative application developer.

## References

1. [Audacity Sound Editor](https://www.audacityteam.org)
2. [Exploring Additive Synthesis Video on YouTube](https://www.youtube.com/watch?v=1ngGaYIzvsU)
