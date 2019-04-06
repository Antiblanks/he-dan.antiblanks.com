---
layout: post
title: "Sound design"
date: 2019-03-15 06:14:00 +0100
categories: [GAM720]
tags: [Diary, Project development]
---

## My experience in week seven

The source material this week was focused on the theory and practice of sound design.

The [Introduction Video by Alcwyn Parker](https://falmouthflexible.instructure.com/courses/296/pages/week-7-introduction?module_item_id=19086) gives a brief overview of sound design. The video opens to state that *the importance of this multifaceted and complex specialism is often overlooked* and I completely agree; in the time I spent building online games I cannot recall one game that had it's own bespoke sound recording, in fact, if I recall correctly, all of the games I built had sound tagged on afterwards and the sound was acquired from a stock library with cost-cutting being at the heart of the decision. The video emphasises the importance of sound design and suggests that, when done right, sound design can *enhance the usability of your app and create more meaningful interactions with the user*. The video then gives some examples of how we can add sound to our apps, stock libraries (as I mentioned above) being one of these, but we are warned off from using stock sound being that it *won’t be as relevant to the overall aesthetic* of our apps and that the originality of our apps *may be diminished somewhat*.

We are then introduced to a paper from 1985 titled 'Earcons and Icons: Their Structure and Common Design Principles' which describes earcons as "nonverbal audio messages used in the user-computer interface to provide information to the user about some computer object, operation, or interaction" (1), and breaks these into two types *representational* which aim to resemble the interaction in some way and *abstract* which are derived from sets of pitches that are said to form motives, where a motive is defined as a "brief succession of pitches arranged to produce a rhythmic and tonal pattern sufficiently distinct to allow it to function as an individual, recognisable entity." (1). The former *representational* being very simple for me to understand but the later by name being more *abstract*. We are given advice about the length of an earcon which *should be sufficient to convey the message effectively, and no longer* and that *the meaning must come across as quickly and as easily as possible* and we are given the paper as reference for further reading with a closing statement to the section which announces the relevance of reading the paper, despite its age.

The video then touches on how modern sound design has moved on from this and how recent advances in Artificial Intelligence (AI) and speech recognition have caused a rise in voice-controlled intelligent personal assistant devices, forcing us as app developers to question traditional interface paradigms and consider what an app design looks like when the Graphical User Interface (GUI) is removed. Considering this myself is important being to ensure that Escape The App's playable element remains non-intrusive I will have to rely heavily on sound to notify the user of changing events that are taking place while the device is nested in the users pocket.

The video then closes with some sound design considerations posed by Hugo Verweij, a sound designer at Apple, who prompts us to question how the UI can benefit from an audible component, suggesting it is vital to find a balance and ensure that all audio is meaningful, and whether sound can play a role in our app's branding which he suggests we should consider from the outset.

The [Introduction to Sound Design Video by Pete Shepherd](https://falmouthflexible.instructure.com/courses/296/pages/week-7-an-introduction-to-sound-design?module_item_id=19090) delves deeper into the fundamentals of audio for games. Shepherd opens to suggest that game audio can be split into three distinct areas combined to give the final product, these being:

- **Composition**: An engaging score making the player experience more immersive.
- **Sound design**: Sounds used to present action on screen.
- **Adaptive elements**: Relating to both, implemented using programs such as [FMod](https://www.fmod.com) or [WWise](https://www.audiokinetic.com/products/wwise), describing sounds that adapt to changes.

The video gives more detail of these three areas and offers *underscores* as an example of composition, being a musical background that underpins the action on screen, *leitmotifs* as an example of sound design, being a musical phrase assigned to a character or scene, and then looks at how we might adapt both of these such as shifting the underscore based on game or player conditions and playing a certain leitmotif when a character enters the screen. The video suggests that we can divide sonic elements in sound design into two basic descriptives. These being *diegetic sounds*, those that relate directly to what we are seeing on screen, and *non-diegetic sounds*, those that do not relate directly to action on screen but rather are used for ambience and scene setting. The video looks at the different ways we can source sound, there is mention of utilising stock sounds but again recording our own sounds is promoted as being more favourable. Finally there are various techniques raised in which we can record sound including *field recording* and *Foley sounds*, *synthesis* and *mimetic sounds*.

The [Foley and Found Sound Content Case Study Videos](https://falmouthflexible.instructure.com/courses/296/pages/week-7-foley-and-found-sound?module_item_id=19091) look at two case studies of professional works, Batman Arkham City by [Rocksteady Games](http://rocksteadyltd.com) and DTS brand sound design by [Diego Stocco](http://www.diegostocco.com). Both are designed to inspire us and instruct us on how we could create Foley sounds. The videos are hugely fascinating and demonstrate the pure genius and creativity behind the craft of creating Foley sound and just how far practitioners are willing to go to add more production value to games and deliver a more convincing experience to the user.

### Tying this to my project

The content over this week has helped me to begin to understand the theory and process behind good sound design and the importance of this element within apps and games. I've certainly been inspired to apply more emphasis on the audio creation for Escape The App to create more meaningful interactions with the user and improve the overall experience.

When considering what sounds are right for Escape The App, I feel that I should avoid any theme based sounds in the composition being that escape rooms all have their own bespoke themes, and in my experiences throughout my research, the rooms will play continuous ambient sound to accompany their theme which would be testing to compliment and avoid conflicting with which would deliver a bad user experience. Saying this, a mixture of diegetic and non-diegetic sound would be preferable as an underscore during game play but the key here is to keep this sound generic and subtle. Above all I would like this sound to heighten the emotion and increase the intensity as the time runs down, potentially the ticking of a clock that gets louder throughout or something similar. I need to consider what sounds I will use to alert the user of game play events such as a new clue becoming available and whether these are mimetic or is this more of a leitmotif for the games master, being that whenever an event occurs the games master will appear to deliver the information.

With regard to the sounds I will use in Escape The App, it's probable that these will be stock sounds that I've edited together, but given how inspired I was by the works of Rocksteady and Diego Stocco, I would like to try my hand at creating some Foley sounds once I clarify exactly what sounds I will need. I will certainly need to record the voice of the games master to deliver all parts of the narrative during game play so I need to work to understand what type of voice this character would have and then set about finding someone to narrate for me.

I've written a more in-depth post on the sound design for Escape The App [here]({% post_url 2019-03-16-week-7-experimenting-with-sounds %}).

## Summary

In this post I've summarised the parts of source material from the week on Canvas that have been most influential to me and I've attempted to use what I've learned to start thinking about what sounds I would like to have in Escape The App and how I would go about sourcing these.

## References

1. [Earcons and Icons Paper](http://www.daimi.au.dk/~dsound/DigitalAudio.dir/Papers/Earcons_and_Icons.pdf)
2. [FMod Website](https://www.fmod.com)
3. [Rocksteady Games Website](http://rocksteadyltd.com)
4. [WWise Product on the Audio Kinetic Website](https://www.audiokinetic.com/products/wwise)
5. [Youtube Instructional Video on Adding Sound with FMod and WWise](https://www.youtube.com/watch?v=S7pL4_yN7RY)
