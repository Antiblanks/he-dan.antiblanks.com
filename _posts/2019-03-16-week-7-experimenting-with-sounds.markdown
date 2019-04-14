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

Unfortunately neither one of these were perfect. The `react-native-sound` library had a more suited interface for my requirements but it had not been maintained for quite some time which may present issues in future. The `react-native-track-player` library was actively being maintained but it didn't satisfy a lot of my requirements. Weighing the two I decided to use `react-native-sound` but anticipated that I may need to fork and maintain the library myself if required.

> Note: Being my sound manager will be an interface that masks the library I leverage it didn't really matter which I used now as this could easily be switched out later without having to rework any control flow.

Once I'd chosen my library to play sound I set about building my adaptive sound manager. I've listed the technical requirements I'd identified the class (or framework) would need to satisfy below. Aside from these requirements I also wanted the solution to be reusable so the interface would need to be more abstract and expose all the methods my game engine needed to combine and deliver the bespoke parts of the control flow:

1. **Pre-loading all sounds**: To ensure all sounds have buffered and are ready for playback on demand during game play.
2. **Playing multiple sounds**: To play the underscore as well as multiple sound effects on top of this during game play.
3. **Switching two sound files**: To change the sound looping in the underscore with the next sound based on the time used during game play.
4. **Increasing the volume**: To increase the sound in the underscore based on the time used during game play.

Here's my solution which I separated into two files:

**SoundUtility**

This is a reusable sound utility module that wraps the `react-native-sound` library and exposes a common interface for the caller to add sounds into channels and control them independently or together. I won't go into much more detail as the code is well commented and speaks for itself.

```
import Sound from 'react-native-sound';
import { mergeRight, mergeDeepRight, pathOr, map, filter, find, forEach } from 'ramda';
import resolveAssetSource from 'react-native/Libraries/Image/resolveAssetSource';

// Enable playback in silence mode
Sound.setCategory('Playback');

/**
 * @function loadNativeSound
 * Load and return a new native sound
 * @param {Object} sound
 * @param {Boolean} autoPlay
 */
export const loadNativeSound = ({ asset, numberOfLoops, volume }, autoPlay = true) => new Promise(
  resolve => {
    const sound = new Sound(asset, (error) => {
      const { uri: assetUri } = resolveAssetSource(asset);
      if (error) {
        console.error(`SoundUtility: Cound not create sound from asset ${assetUri}.`);
        resolve(null);
        return undefined;
      }
      sound.setVolume(volume);
      sound.setNumberOfLoops(numberOfLoops);
      // NOTE: Playing then stopping a sound immediately fixes the looping issue
      // As described in this ticket https://github.com/zmxv/react-native-sound/issues/31
      autoPlay ? sound.play() : sound.play().stop();
      resolve(sound);
    });
  }
);

/**
 * @class SoundUtility
 * TODO: Need to add unit tests for this utility
 */
export default class {
  /**
   * @var sounds
   * Sounds map to store all registered sounds
   */
  sounds = {};

  /**
   * @var channels
   * This allows us to play sounds on different channels
   */
  channels = {};

  constructor(channels = []) {
    forEach((channel) => this.channels[channel] = {}, channels);
  }

  // Private

  /**
   * @function _getNativeSound
   * Checks whether the sound is valid and returns the native sound
   * @param {String} id
   * @param {String} action
   */
  _getNativeSound(id = undefined, action = 'play') {
    const sound = pathOr(null, [id, 'sound'], this.sounds);
    if (!sound) {
      console.error(`SoundUtility: Cannot call ${action} on sound with id ${id}.`);
      return null;
    }
    return sound;
  }

  // Public

  /**
   * @function addNewSound
   * Adds a new game sound to the managed sounds map
   * @param {String} id
   * @param {Object} asset
   * @param {String} channel
   * @param {Number} numberOfLoops
   * @param {Number} volume
   * @param {Boolean} autoPlay
   */
  addNewSound(id, asset, channel, numberOfLoops = -1, volume = 1, autoPlay = true) {
    if (!asset) {
      console.warn(`SoundUtility: Attempting to add sound with invalid asset ${asset}.`);
      return null;
    }
    const isValidChannel = pathOr(false, [channel], this.channels);
    if (!isValidChannel) {
      console.warn(`SoundUtility: Attempting to add sound to invalid channel ${channel}.`);
      return null;
    }
    const existingSound = pathOr(null, [id], this.sounds);
    if (existingSound) {
      // TODO: Need to support playing the same sound in a different channel
      // NOTE: This is not a requirement for now but it might be later
      return existingSound;
    }
    const newSound = { id, asset, channel, numberOfLoops, volume };
    this.sounds = mergeRight(this.sounds, { [id]: newSound });
    this.channels = mergeDeepRight(this.channels, { [channel]: { id } });
    loadNativeSound({ asset, numberOfLoops, volume }, autoPlay).then((nativeSound) => {
      // Make sure the sound is still being managed, otherwise release the native sound and exit
      const sound = pathOr(null, [id], this.sounds);
      if (!sound) {
        nativeSound.release();
        return undefined;
      }
      this.sounds = mergeRight(this.sounds, {
        [id]: mergeRight(sound, { sound: nativeSound })
      });
    });
    return newSound;
  }

  /**
   * @function playNewSound
   * Adds a new sound to the managed sounds map and plays it immediately
   * @param {String} id
   * @param {Object} asset
   * @param {String} channel
   * @param {Number} numberOfLoops
   * @param {Number} volume
   * @param {Boolean} autoPlay
   */
  playNewSound(id, asset, channel, numberOfLoops = -1, volume = 1, autoPlay = true) {
    const newSound = this.addNewSound(id, asset, channel, numberOfLoops, volume, autoPlay);
    if (!newSound) {
      return undefined;
    }
    this.playSound(id);
  }

  /**
   * @function play
   * Plays an existing sound from sounds map by key
   * @param {String} id
   */
  play(id = undefined) {
    const nativeSound = this._getNativeSound(id, 'play');
    if (!nativeSound) return undefined;
    nativeSound.play();
  }

  /**
   * @function pause
   * Pauses an existing sound from sounds map by key
   * @param {String} id
   */
  pause(id = undefined) {
    const nativeSound = this._getNativeSound(id, 'pause');
    if (!nativeSound) return undefined;
    nativeSound.pause();
  }

  /**
   * @function stop
   * Stops an existing sound from sounds map by key
   * @param {String} id
   */
  stop(id = undefined) {
    const nativeSound = this._getNativeSound(id, 'stop');
    if (!nativeSound) return undefined;
    nativeSound.stop();
  }

  /**
   * @function release
   * Releases an existing sound from sounds map by key
   * @param {String} id
   */
  release(id = undefined) {
    const nativeSound = this._getNativeSound(id, 'release');
    if (!nativeSound) return undefined;
    nativeSound.release();
  }

  /**
   * @function isPlaying
   * Returns whether an existing sound from sounds map by key is playing or not
   * @param {String} id
   */
  isPlaying(id = undefined) {
    const nativeSound = this._getNativeSound(id, 'isPlaying');
    if (!nativeSound) return false;
    return nativeSound.isPlaying();
  }

  /**
   * @function playAll
   * Plays all existing sounds in map
   */
  playAll() {
    map(({ id }) => this.play(id), this.sounds);
  }

  /**
   * @function pauseAll
   * Pauses all existing sounds in map
   */
  pauseAll() {
    map(({ id }) => this.pause(id), this.sounds);
  }

  /**
   * @function stopAll
   * Stops all existing sounds in map
   */
  stopAll() {
    map(({ id }) => this.stop(id), this.sounds);
  }

  /**
   * @function releaseAll
   * Releases all existing sounds in map
   */
  releaseAll() {
    map(({ id }) => this.release(id), this.sounds);
  }

  /**
   * @function playChannel
   * Plays all existing sounds in channels map
   * @param {String} channel
   */
  playChannel(channel) {
    map((id) => this.play(id), pathOr({}, [channel], this.channels));
  }

  /**
   * @function pauseChannel
   * Pauses all existing sounds in channels map
   * @param {String} channel
   */
  pauseChannel(channel) {
    map((id) => this.pause(id), pathOr({}, [channel], this.channels));
  }

  /**
   * @function stopChannel
   * Stops all existing sounds in channels map
   * @param {String} channel
   */
  stopChannel(channel) {
    map((id) => this.stop(id), pathOr({}, [channel], this.channels));
  }

  /**
   * @function releaseChannel
   * Releases all existing sounds in channels map
   * @param {String} channel
   */
  releaseChannel(channel) {
    map((id) => this.release(id), pathOr({}, [channel], this.channels));
  }

  /**
   * @function getSoundsPlayingInChannel
   * Return all sounds playing in the specified channel
   * @param {String} channel
   */
  getSoundsPlayingInChannel(channel) {
    return filter((id) => this.isPlaying(id), pathOr({}, [channel], this.channels));
  }

  /**
   * @function getSoundPlayingInChannel
   * Return a sound matching id that is playing in the specified channel
   * @param {String} channel
   * @param {String} matchId
   */
  getSoundPlayingInChannel(channel, matchId) {
    return find((id) => id === matchId && this.isPlaying(id), pathOr({}, [channel], this.channels));
  }

  /**
   * @function replaceSoundPlaying
   * Replace a sound playing with another sound
   * @param {String} oldId
   * @param {String} newId
   */
  replaceSoundPlaying(oldId, newId) {
    if (this.isPlaying(oldId)) this.stop(oldId);
    if (!this.isPlaying(newId)) this.play(newId);
  }
};

```

**GameSoundUtility**

This is a decorator for the `SoundUtility`, it's lightweight and it's sole purpose is to extend the `SoundUtility` and predefine two channels that are relevant to games. To summarise the `SoundUtility` houses the low level abstract functionality that would be useful for working with sounds in any app but the `GameSoundUtility` houses any game specific sound concerns.

```
import SoundUtility from 'App/Utilities/SoundUtility';

export const CHANNEL_UNDERSCORE = 'underscoreChannel';
export const CHANNEL_SOUND_EFFECTS = 'soundEffectsChannel';

class GameSoundUtility extends SoundUtility {
  _instance = null;

  constructor() {
    super([
      CHANNEL_UNDERSCORE,
      CHANNEL_SOUND_EFFECTS
    ]);
  }

  static getInstance() {
    if (!this._instance) {
      this._instance = new GameSoundUtility();
    }
    return this._instance;
  }

  /**
   * @function playUnderscore
   * Plays all sounds in the underscore channel map
   */
  playUnderscore() {
    this.playChannel(CHANNEL_UNDERSCORE);
  }

  /**
   * @function pauseUnderscore
   * Pauses all sounds in the underscore channel map
   */
  pauseUnderscore() {
    this.pauseChannel(CHANNEL_UNDERSCORE);
  }

  /**
   * @function stopUnderscore
   * Stops all sounds in the underscore channel map
   */
  stopUnderscore() {
    this.stopChannel(CHANNEL_UNDERSCORE);
  }

  /**
   * @function playSoundEffects
   * Plays all sounds in the sound effects channel map
   */
  playSoundEffects() {
    this.playChannel(CHANNEL_SOUND_EFFECTS);
  }

  /**
   * @function pauseSoundEffects
   * Pauses all sounds in the sound effects channel map
   */
  pauseSoundEffects() {
    this.pauseChannel(CHANNEL_SOUND_EFFECTS);
  }

  /**
   * @function stopSoundEffects
   * Stops all sounds in the sound effects channel map
   */
  stopSoundEffects() {
    this.stopChannel(CHANNEL_SOUND_EFFECTS);
  }

  /**
   * @function getSoundsPlayingInUnderscore
   * Return all sounds playing in the underscore channel
   */
  getSoundsPlayingInUnderscore() {
    return this.getSoundsPlayingInChannel(CHANNEL_UNDERSCORE);
  }
};

export default GameSoundUtility;
```

My caller, which in this case was the `GameSaga` that houses my game control flow could then construct the flow required by the game and play the sounds required using a singleton instance of the `GameSoundUtility`, for example:

**Loading sounds on initialisation**

```
const SOUND_UNDERSCORE_LOW = `underscore--low`;
const SOUND_UNDERSCORE_MEDIUM = `underscore--medium`;
const SOUND_UNDERSCORE_HIGH = `underscore--high`;

GameSoundUtility.getInstance().addNewSound(
  SOUND_UNDERSCORE_LOW, Sounds.game.underscore.low, CHANNEL_UNDERSCORE, -1, 0.25, false
);

GameSoundUtility.getInstance().addNewSound(
  SOUND_UNDERSCORE_MEDIUM, Sounds.game.underscore.medium, CHANNEL_UNDERSCORE, -1, 0.25, false
);

GameSoundUtility.getInstance().addNewSound(
  SOUND_UNDERSCORE_HIGH, Sounds.game.underscore.high, CHANNEL_UNDERSCORE, -1, 0.25, false
);
```

**Playing the first sound on the underscore channel upon game start**

```
/**
 * @generator startGame
 * Saga generator function to start a new game
 */
export function* startGame() {
  const game = yield select(selectedGameSelector);
  if (!game) {
    yield put(GameActions.startGameFailed());
    return undefined;
  }
  const { maxTimeAllowedInMs: startTime } = game;
  yield put(GameActions.startGameSuccess(startTime));
  NavigationService.navigate(ScreenTypes.GAME_PLAY_SCREEN_KEY);
  GameSoundUtility.getInstance().play(SOUND_UNDERSCORE_LOW);
  const channel = yield call(countdown, startTime);
  try {
    while (true) {
      const currentTime = yield take(channel);
      yield fork(updateGame, { currentTime });
    }
  }
  finally {
    yield fork(endGame);
  }
}
```

**Changing the sound on the underscore channel based on the time used**

```
/**
 * @generator _updateGameChangeUnderscore
 * Saga generator function to change the underscore on game update
 * @param {Object} game
 * @param {Number} currentTime
 */
function* _updateGameChangeUnderscore({ game, currentTime }) {
  const { maxTimeAllowedInMs } = game;
  const timeUsedInMs = maxTimeAllowedInMs - currentTime;
  const timeToPlayHighSound = (maxTimeAllowedInMs / 3) * 2;
  if (timeUsedInMs >= timeToPlayHighSound) {
    GameSoundUtility.getInstance().replaceSoundPlaying(SOUND_UNDERSCORE_MEDIUM, SOUND_UNDERSCORE_HIGH);
    return undefined;
  }
  const timeToPlayMediumSound = maxTimeAllowedInMs / 3;
  if (timeUsedInMs >= timeToPlayMediumSound) {
    GameSoundUtility.getInstance().replaceSoundPlaying(SOUND_UNDERSCORE_LOW, SOUND_UNDERSCORE_MEDIUM);
  }
};

/**
 * @generator updateGame
 * Saga generator function to update a game
 * @param {Number} currentTime
 */
export function* updateGame({ currentTime }) {
  const game = yield select(selectedGameSelector);
  if (!game) {
    stopCountdown();
    return undefined;
  }
  yield call(_updateGameGiveClue, { game, currentTime });
  yield call(_updateGameChangeUnderscore, { game, currentTime });
  yield put(GameActions.updateGameTime(currentTime));
}
```

And that's how I've added the underscore sounds into my MVP version of the game. It's not a complete solution and there are some further improvements required. A keen eye will have spotted the `TODO` comments in my code that I've left by choice as they don't block completion of Escape The App so I've left these for the time being but will look to address these later when required. Aside from this there is one big challenge yet to face and this is that (unless I'm incredibly lucky) this solution will not play sounds in the background and this is, as I've stated on numerous occasions, imperative to delivering a good game play experience.

> Additionally: I learned while writing this post that WAV files loop better than MP3 files. I didn't know this before but the lossless PCM WAV format is the best format for loops, and that many lossy, compressed formats like MP3, WMA and ADPCM WAV suffer from added silence at the the start or end of the file that do not respect the exact length.

### Sound design, leitmotif or mimetic, diegetic

TODO...

## Summary

In this post I've TODO...

In hindsight the fire alarm sound might be distracting, verify this during play test

HIghlights that React Native though fine for my app might not be the best choice for building a more complicated game but should investigate https://github.com/bberak/react-native-game-engine




## References

1. [Audacity Sound Editor](https://www.audacityteam.org)
2. [Audio Libraries in React Native Post on Medium](https://medium.com/@emmettharper/the-state-of-audio-libraries-in-react-native-7e542f57b3b4)
3. [Richard Branson on Quotes About Ideation](https://www.virgin.com/richard-branson/my-top-10-quotes-ideas)
4. [Sound Bible Stock Sounds Website](http://soundbible.com)
5. [Timer Sound on YouTube](https://www.youtube.com/watch?v=qjqZqpmaVks)
