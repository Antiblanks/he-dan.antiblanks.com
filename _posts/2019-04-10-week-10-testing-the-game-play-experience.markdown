---
layout: post
title: "Testing the gameplay experience"
date: 2019-04-10 06:18:00 +0100
categories: [GAM720]
tags: [Diary, Project development]
---

Being I reached the end of this week with a near end-to-end first version of the gameplay experience, I decided it was a good time to bring some user testing into scope to get some feedback to improve parts of this feature ahead of my submission in three weeks. As I touched on in this [post]({% post_url 2019-03-23-week-8-creating-brand-and-notification-sounds %}) about developing the gameplay journeys there are two types of game, I will list these with definitions below:

- **Unsubscribed games**: These are games that are manually added into the app or scraped. These games comprise of basic public data that is easily obtainable online such as the time allowed to escape the game and the minimum and maximum number of players. An unsubscribed game can be played but the experience is stripped down to allow the player to record their escape time and save it but there will be no clues available.
- **Subscribed games**: These are unsubscribed games that have been enriched with their rooms and the clues in each room by the game owners. A subscribed game can be played with all the same functionality as an unsubscribed game but in this case the user is given advice about their progress throughout a game, and the clues that were added are made available at the time stated upon entry. Once a clue has been made available it can be taken immediately or it can be taken later from within the available clues dialog. Taking a clue carries an optional time penalty that can be added by the game owner.

The focus of this user testing was to test both these types of game with a handful of users and observe how they interact with each game and then conduct a short informal interview afterwards to get feedback so that I could then make steps to improve the games in certain areas.

I've documented the complete results of the test [here](http://projects.antiblanks.com/escape/testing/Escape_UserTesting--PlayingAGame-20190401.pdf) but to summarise here are some of the key takeaways accompanied by my suggestions to remedy the problem areas:

### The countdown screen

![](/assets/img/GAM720_Wk10_TestingGamePlay--001.png)

**Observation / feedback**: One test subject instinctively clicked the 'Stop' button on the countdown timer screen to stop the game from starting. On questioned why he did this after the test was complete, the subject suggested this was because the button was quite prominent and he thought it was the required thing to do to start the game immediately without waiting for the countdown to complete.

**Solution**: In my opinion the issue with the 'Stop' button is that it has the same styling as a main CTA button. From a design language point of view all buttons that look like this in the app instigate the most intuitive action. In the case of a confirmation scenario in the app the main CTA will confirm and there is a secondary CTA beneath this to cancel. One solution to this problem is to make this button a main CTA with the label 'Start the game already!' (or similar) and give it the positive outcome the user was looking for, and then add a secondary CTA beneath the main CTA which reads 'Cancel' that is more consistent with the language used everywhere else in a confirm or cancel scenario. I have created a ticket on Trello [here](https://trello.com/c/J4S26BaR/55-dev019-alter-the-design-language-of-the-stop-button-on-the-countdown-screen) to address this.

### Playing an unsubscribed game

![](/assets/img/GAM720_Wk10_TestingGamePlay--002.png)

**Observation / feedback**: All subjects paused for a while once the game had begun and then started looking for what they should do next. One test subject handed the phone back as if the test had finished. When question on this afterwards the consensus was that they were a bit confused about what they were supposed to do next. When I told the subjects that they could have locked the phone and played the game while the timer ran down in their pocket they said that this was not clear.

**Solution**: The
