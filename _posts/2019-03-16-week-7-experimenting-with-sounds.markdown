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

A Google search for 'Anxious sounds' led me on a path of discovery to identify ringing alarms sounds such as car and burglar alarms but this type of sound is consistent (not building) and more akin to a climactic situation, in my app perhaps more suited to the time having ran out but not running down. This prompted me to consider the function of an old fashioned egg timer that makes a consistent ticking noise as the time runs down and then sounds an alarm when the time runs out, but though this builds anticipation, the sound doesn't build in intensity, it is instead consistent with a sudden climax. I then considered the solution of using a timer ticking sound and the potential of starting this as a quieter single repetitive sound but intensifying the sound by increasing the volume and layering the sounds as time goes on, so it would start barely noticeable but sound like an alarm by the time it had reached it's end. Of course this seemed a bit obvious but as Sir Richard Branson can attest the [simple ideas are often the best](https://www.virgin.com/richard-branson/my-top-10-quotes-ideas).

My vision for the ticking underscore was to replicate the arrangement of an analogue clock ticking to emphasise the passing of time but replace the different parts within the composition with a variant of digital (potentially mimetic) beeping sounds that when increased in volume and layered up will sound like an alarm. I found this [clock animation](https://www.youtube.com/watch?v=qjqZqpmaVks) on YouTube that helped me to understand the combination of sounds that are required and how they need to be arranged to portray a clock ticking. I then set about acquiring my own sounds, despite being warned off using stock sounds because they lack originality, I used a handful of sounds I found on [Sound Bible](http://soundbible.com) for experimentation with a view that I could record my own sounds to replace these if after being combined the overall composition didn't sound to my liking. I opted for the high pitched beep of a house firm alarm, a low pitched morse code transmitter and a mid-pitch electrical test sensor. I then brought these sounds into [Audacity](https://www.audacityteam.org) and cut them up and arranged them to replicate the sound of a ticking clock.

**Creating the two millisecond ticks**

The clock example has a repetitive fast paced low volume tick that appears to sound five times within each second. Representing this was the first step. To do this I imported the mid-pitch electrical test sensor snippet, I increased the speed, to create a higher pitched shorter chirp exactly two milliseconds in length and I lowered the gain to make the sound more subtle and then duplicated this.

![](/assets/img/GAM720_Wk7_Audacity--001.png)

![](/assets/img/GAM720_Wk7_Audacity--002.png)

**Creating the high pitch one second tick**

Next I set about recreating the sound of the tick that happens every second. Initially I used the fire alarm snippet which I trimmed to four milliseconds to span the duration of two of the two millisecond ticks and I increased the gain to apply more weight and impact to this sound.

![](/assets/img/GAM720_Wk7_Audacity--003.png)

**Creating the mid-range one second tick**

Next I wanted to intensify the sound of the tick that happens every second. I did this by bringing over the morse code transmitter snippet and trimming this to use just one beep in the wave form. I trimmed this and increased the pitch to match the duration of the two millisecond tick and tweaked the gain a little to make this sound sit somewhere in between the range created by the first two sounds.

![](/assets/img/GAM720_Wk7_Audacity--004.png)

Finally I tweaked the gain of all seven tracks so that the composition sounded nice and tight and I started muting the two sounds used to represent the one second tick to decide the order in which I would layer the sounds up to incrementally intensify the underscore and build the sound of the alarm. Here are the three sound recordings I will use to do this:

1. [Two millisecond ticks](/assets/sound/GAM720_Wk7_Underscore--001.mp3)
2. [Two millisecond ticks with mid-range one second tick](/assets/sound/GAM720_Wk7_Underscore--002.mp3)
3. [Two millisecond ticks with mid-range and high pitch one second tick](/assets/sound/GAM720_Wk7_Underscore--003.mp3)

**Bringing the sounds into my app**

Unfortunately React Native is not geared toward building games like Unity or Unreal Engine and as far as I could see there is no pre-existing game-centric adaptive sound manager available, so I settled on building my own sound manager to adapt my sounds during game play. I didn't want to reinvent the wheel completely of course so I did some research and this [article](https://medium.com/@emmettharper/the-state-of-audio-libraries-in-react-native-7e542f57b3b4) on Medium gave me some insight into the libraries available for working with sound and indicated these two as being the most relevant for my app:

- [React Native Sound](https://github.com/zmxv/react-native-sound)
- [React Native Track Player](https://react-native-kit.github.io/react-native-track-player)

> In doing this research I was faced with the challenge of playing sound in the background TODO...

Once I'd chosen my library to play sound I set about building my adaptive sound manager. My intention was to create an adaptive underscore that switches the sound recording and increases the volume in response to changes in the game timer. Technically speaking this could be broken into three parts:

1.
2. **Switching the sound file**: I will want to take the `maxTimeAllowedInMs` property from the active game, divide this by the number of sound files (3) and then load the correct sound file based on the players `timeUsedInMs` property.
3. **Increasing the volume**: I will want to to take the `maxTimeAllowedInMs` property from the active game

### Sound design, leitmotif or mimetic, diegetic

TODO...

## Summary

In this post I've TODO...

In hindsight the fire alarm sound might be distracting, verify this during play test

HIghlights that React Native though fine for my app might not be the best choice for building a more complicated game but should investigate https://github.com/bberak/react-native-game-engine

Has it's drawbacks, could write some unit tests for GameSoundUtility, doesn't currently allow playing the same sound in a different channel

Discovered that WAV's loop better than MP3: The lossless PCM WAV format is the best format for loops. Choose "WAV (Microsoft) signed 16-bit PCM" when exporting. Many lossy, size-compressed formats like MP3, WMA and ADPCM WAV suffer from added silence at the the start or end of the file or other issues that do not respect the exact length.

I will need to add a sound on/off button



## References

1. [Audacity Sound Editor](https://www.audacityteam.org)
2. [Audio Libraries in React Native Post on Medium](https://medium.com/@emmettharper/the-state-of-audio-libraries-in-react-native-7e542f57b3b4)
3. [Richard Branson on Quotes About Ideation](https://www.virgin.com/richard-branson/my-top-10-quotes-ideas)
4. [Sound Bible Stock Sounds Website](http://soundbible.com)
5. [Timer Sound on YouTube](https://www.youtube.com/watch?v=qjqZqpmaVks)
