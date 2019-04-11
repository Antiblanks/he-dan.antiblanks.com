---
layout: post
title: "Experimenting with sounds"
date: 2019-03-16 07:18:00 +0100
categories: [GAM720]
tags: [Diary, Project development]
---

The sound design for Escape The App has been in the back of my mind for quite some time now. A sound to notify the user when a new clue has been made available during game play is (without question in my opinion) absolutely essential being I anticipate the device is likely to be nested in the users pocket most of the time. Aside from this I'd always felt that a score to underpin the game play experience would be good to build intensity and emphasise urgency as time runs down, however I'd anticipated the difficulty of creating something that would compliment the existing ambience of the rooms. I touched on this [here]({% post_url 2019-03-15-week-7-sound-design %}) when I stated that *I should avoid any theme based sounds in the composition being that escape rooms all have their own bespoke themes, and in my experiences throughout my research, the rooms will play continuous ambient sound to accompany their theme which would be testing to compliment and avoid conflicting with which would deliver a bad user experience*. Bearing this in mind I can summarise my initial sound design requirements for MVP into the below statements with intention to expand upon these later during play testing:

- **Composition, underscore, non-diegetic**: I want to create a score to underpin game play that heightens in intensity over the course of the game as the game timer runs down.
- **Sound design, leitmotif or mimetic, diegetic**: I want to create a sound to highlight that a new clue has been made available during game play.

I considered each of these requirements in more depth to brainstorm potential solutions and I've documented this below.

### Composition, underscore, non-diegetic

A Google search for 'Anxious sounds' led me on a path of discovery to identify ringing alarms sounds such as car and burglar alarms but this type of sound is consistent (not building) and more akin to a climactic situation, in my app perhaps more suited to the time having ran out but not running down. This prompted me to consider the function of an old fashioned egg timer that makes a consistent ticking noise as the time runs down and then sounds an alarm when the time runs out, but though this builds anticipation, the sound doesn't build in intensity, it is instead consistent with a sudden climax. I then considered the solution of using a timer ticking sound and the potential of starting this as a low sound but intensifying the sound by increasing the pitch as time goes on, so it would start barely noticeable but sound like an alarm by the time it had reached it's end. Of course this seemed a bit obvious but as Sir Richard Branson can attest the [simple ideas are often the best](https://www.virgin.com/richard-branson/my-top-10-quotes-ideas).

My vision for the ticking underscore was to replicate the arrangement of an analogue clock ticking to emphasise the passing of time but replace the different parts within the composition with a variant of digital (potentially mimetic) beeping sounds that when increased in pitch will sound like an alarm. I found this [clock animation](https://www.youtube.com/watch?v=qjqZqpmaVks) on YouTube that helped me to understand the combination of sounds that are required and how they need to be arranged to portray a clock ticking. I then set about acquiring my own sounds, despite being warned off using stock sounds because they lack originality, I used a handful of sounds I found on [Sound Bible](http://soundbible.com) for experimentation with a view that I could record my own sounds to replace these if when combined these didn't yield something that sounded original. I opted for the beep of a house firm alarm, a morse code transmitter and an electrical test sensor. I then brought these sounds into [Audacity](https://www.audacityteam.org) and cut them up and arranged them to replicate the sound of the ticking clock. 

### Sound design, leitmotif or mimetic, diegetic

TODO...

## Summary

In this post I've TODO...

## References

1. [Audacity Sound Editor](https://www.audacityteam.org)
2. [Richard Branson on Quotes About Ideation](https://www.virgin.com/richard-branson/my-top-10-quotes-ideas)
3. [Sound Bible Stock Sounds Website](http://soundbible.com)
4. [Timer Sound on YouTube](https://www.youtube.com/watch?v=qjqZqpmaVks)
