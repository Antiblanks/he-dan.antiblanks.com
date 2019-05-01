---
layout: post
title: "Sound process"
date: 2019-03-23 15:35:00 +0100
categories: [GAM720]
tags: [Diary, Project development]
---

## My experience in week eight

The source material this week was focused on the fundamental building blocks of sound through the lens of sound synthesis.

The [Introduction Video by Alcwyn Parker](https://falmouthflexible.instructure.com/courses/296/pages/week-8-introduction?module_item_id=19099) describes the term sound synthesis as being *the practice of generating sound from scratch* and suggests that there are two strands of sound synthesis: *Recreating real-world acoustic sounds* and *Creation of new sounds with unique and other-worldly timbres*. The video goes on to introduce us to a text by Andy Farnell called *Designing Sound* giving a quote from his book that champions sound synthesis in saying that *sounds constructed are more realistic and useful than recordings because they capture behaviour*, and describes Farnell's suggestion that there are three pillars of designing for sounds, these being physics, mathematics and psychology. The video summarises the relationship between programming and sound synthesis and introduces us to Dr Norah Lorway who is an expert in the field of [Live Coding](https://en.wikipedia.org/wiki/Live_coding) and [Algorave](https://en.wikipedia.org/wiki/Algorave). The video references Virtual Reality (VR), mentioning some of the sound synthesis challenges that have been brought about by this technology and highlighting Head Related Transfer Functions (HRTFs) as one solution that is used to make audio in VR more immersive. The video closes by stating that sound synthesis is a great way to design sound for our apps being it doesn't involve field recording or require studio equipment and that there are a range of open-source tools we can use to experiment with and generate interesting sounds. We are warned that sound synthesis is a complex field, can feel daunting to approach and that the results can sound artificial but encouraged to experiment and make some noise.

The [BBC Radiophonic Workshop Video](https://falmouthflexible.instructure.com/courses/296/pages/week-8-bbc-radiophonic-workshop?module_item_id=19103) introduces us to the [BBC Radiophonic Workshop](https://en.wikipedia.org/wiki/BBC_Radiophonic_Workshop) which was created in 1958 to make electronic music for radio and television programmes. The video summarises how an electronic synthesiser device can be used to create sounds, taking us through the function of the oscillators, adjusting pitch and volume and explaining how this can be visualised on the oscilloscope. The video demonstrates how oscillators can be used to control one other and create a vibrato effect. We are taken through the workings of the patch board and how this can be used to introduce new oscillators and different single sounds with basic tones and harmonics, we are then taken through the envelope shaper controls which are used to shape notes by introducing attack and delay, and finally we are taken through the use of high pass and low pass filters to cut out notes in a chord. The video closes by demonstrating how the sounds we've heard can be combined to create a melody and there's an example of how this was put to use in a television programme.

The [Live Coding and Algorave Video by Dr Norah Lorway](https://falmouthflexible.instructure.com/courses/296/pages/week-8-live-coding-and-algoraves?module_item_id=19104) gives us more insight into her work, her involvement with creating 3D printed wearables for sound and her work with live coding and how she's been inspired to work with the gestural control of sound both with the body and with other types of apparatus. We are introduced to [SuperCollider](https://en.wikipedia.org/wiki/SuperCollider), the environment and programming language that Dr Norah Lorway uses to create sound and which she uses amongst other coding languages for live coding performances. The remainder of the video is aimed at algorave that Dr Lorway describes as live music events that include dancing. I'm no stranger to algorave, I've never been to one but I do know what they are, I've watched videos and I respect the work of the artists who are involved in this. I've thought about giving it a go being I like both dance music and coding but I'm a very visual person and I get satisfaction from making things that look nice, and though I understand the importance of sound within apps, I think live coding is perhaps more for those who are passionate about sound and music and that's really not me.

The final focus of the weeks content was directed toward giving us an introduction to [Sonic PI](https://sonic-pi.net) and setting us a task to create an audio logo and notifications for our app.

### Tying this to my project

Parts of the content this week were highly relevant to my development work on Escape The App, particularly the task to create an audio logo and notification sounds. Though I wasn't convinced I needed sound to accompany my app logo, the idea of exploring this did appeal being that I could add this to my existing splash screen which might help to create intrigue for new users and add a touch of production value to the app. There's argument of course to state that the splash screen should be as light weight as possible, and reducing asset load on this screen is preferable, but a small sound file of a few seconds would be pretty lightweight so I decided to experiment with this. Aside from this, and definitely of more importance to my app is the creation of notifications as I already acknowledged in this [post]({% post_url 2019-03-15-week-7-sound-design %}) that I would need a sound to notify the user of a clue being made available and I had a task to tackle this on Trello [here](https://trello.com/c/UVtMG8yR/50-dev016-add-haptic-feedback-and-mimetic-sound-when-clue-is-available) so this seemed like a good time to do this. I've written a more in depth post on this [here]({% post_url 2019-03-23-week-8-creating-brand-and-notification-sounds %}).

## Summary

In this post I've summarised the weeks content and I've detailed how relevant the task to create an audio logo and notification sounds were to my development on Escape The App. I've directly related this activity to a task I'd already created on Trello and I've taken the opportunity to complete the task using my learning from this weeks source material.

## References

1. [Algorave Wikipedia Page](https://en.wikipedia.org/wiki/Algorave)
2. [BBC Radiophonic Workshop Wikipedia Page](https://en.wikipedia.org/wiki/BBC_Radiophonic_Workshop)
3. [Live Coding Wikipedia Page](https://en.wikipedia.org/wiki/Live_coding)
4. [Sonic PI Website](https://sonic-pi.net)
5. [SuperCollider Wikipedia Page](https://en.wikipedia.org/wiki/SuperCollider)
