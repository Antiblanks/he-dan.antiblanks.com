---
layout: post
title: "Developing the game play journey's"
date: 2019-04-09 06:16:00 +0100
categories: [GAM720]
tags: [Diary, Project development]
---

My early research into the play of escape games indicated that escape game enthusiasts are highly competitive and have a strong will to play against one another to escape games in the least amount of time possible. This discovery was the foundation for building Escape The App which aims to bring gamification to the physical experience of playing escape games and satisfying the competitive nature of my users is at the heart of every decision I make when approaching the development of the product.

When I started this twelve week module my opinion was that the companion playable element to the physical escape game was the core feature from which everything else in my app would extend. The playable element is responsible for standardising the score which is the foundation for gamification and my feeling was that the playable element was the hook that would create stickiness for the escape game enthusiast users. For this reason my drive over this study block has been to create an MVP that focuses on delivering basic but complete end-to-end journey's that allow the user to register, find a game, play a game and then save their score. Playing a game was such a big part of this that I've been developing it alongside everything else to give each facet of the solution time to distill and improve.

### Early UX for the playable element

The article below shows the UX that I used to instigate the development of the playable experience. At time of drafting this I had no understanding how important narrative was within my app and the notion of suspending disbelief was not even a consideration at this point. The result of course is that the UX is quite flat, all the functionality required is present and relevant but I felt it lacked the depth required to be considered a strong execution. Despite this I based my development on this UX and I iterated and improved the solution as I learned more throughout the study block.

![](/assets/img/GAM720_Wk10_GamePlay--001.png)

### Improved playable experience

After several iterations the below journey's summarise how the playable experience looks today, there has not been a vast departure within the overarching flows but having realised the importance of narrative in achieving stickiness which I first touched on in this [post]({% post_url 2019-03-01-week-5-concept-art %}), I've considered the messaging in much greater depth and devised a vessel to deliver this as described in this [post]({% post_url 2019-03-21-week-8-revising-the-narrative-delivery %}) and weaved the storyline into the game. Also, having played numerous escape games for research purposes since the creation of the initial UX, I've improved minor details in the content, design and animation to enhance the experience to better fulfil it's purpose.

**Starting a new game**

This journey has remained completely untouched and is exactly the same as in the original UX.

![](/assets/img/GAM720_Wk10_GamePlay--002.png)

**Taking a newly available clue**

This journey was not present in the original UX but was introduced as it was deemed during development testing that changes in the clue area when a clue becomes available were not apparent enough and new clues could go unseen. User feedback from playing games for research also highlighted that users would be far too involved in the physical aspect of playing a game that they would unlikely be holding their device, for this reason, if the app is active when a new clue is made available the visual notification is shown, however if the app is inactive the user will be notified of the new clue using haptic feedback accompanied by a mimetic sound and the message will be shown upon re-activating the app.

![](/assets/img/GAM720_Wk10_GamePlay--003.png)

**Taking a previously available clue**

This journey has remained largely unchanged from the original UX, however it became apparent during development testing that there was a flow missing for users who want to take a clue they've already seen. To satisfy this I created the following [task](https://trello.com/c/svnVmXkA/49-dev015-add-clue-list-item-state-for-clue-that-has-been-taken) on Trello to alter the display of a clue in the available clues list to communicate to the user that the clue can be seen again with no further time penalty and altered the logic to skip the confirmation step if the clue had already been taken.

![](/assets/img/GAM720_Wk10_GamePlay--004.png)

**Quitting a game**

User testing highlighted that the quit button (despite small) could be clicked by mistake which in turn would quit the game prematurely with no way for them to prevent this. To counter this I've added a step to check that the user wants to quit which gives them the option to cancel. Upon clicking cancel the user is returned to the game that has continued to run in the background.

![](/assets/img/GAM720_Wk10_GamePlay--005.png)

**Finishing a game**

User testing highlighted that the finish button could quite easily be clicked by mistake which in turn would finish the game prematurely with no way for them to prevent this. To counter this I've added a step to check that the user wants to finish, the escape time is captured upon click and the game timer runs in the background so that the escape time is not frozen if the user decides to cancel finishing and then continue the game. Upon confirming the request to finish a game the users escape time is saved which updates their rank and badges and returns these to be displayed on the `GameFinishedScreen` as a reward for their achievement and accompanied by a customised message to boost the users feeling of heroism.

![](/assets/img/GAM720_Wk10_GamePlay--006.png)

**Playing an unsubscribed game**

Audience research indicated that not allowing a game to be played unless it was added by a subscribing owner would be quite off putting for the escape game player and would be viewed as a barrier to gaining traction. For this reason I aim to add all the games manually which will allow players to find and play every game and submit their score against a game but that scores submitted for unsubscribed games will remain unverified until the owner has subscribed the game. Unsubscribed games have a far less comprehensive experience being that the characteristics of the game are unknown there are no clues given but the playable element is reduced to recording an escape time that can then be saved.

![](/assets/img/GAM720_Wk10_GamePlay--007.png)

### Technical solution

The technical solution for the gameplay element is built using Redux and Redux Saga. At the heart of the playable experience is the `InitialState` for the game. This object defines the properties that can be altered during gameplay to support the gameplay mechanic.

```
export const INITIAL_STATE = {
  selected: null,
  status: null,
  startTime: null,
  currentTime: null,
  finishTime: null,
  clueToGive: null,
  cluesGiven: null,
  cluesTaken: null,
  sending: false,
  error: null
};
```

The control flow for the game engine is defined in the `GameSaga`. Upon starting a new game the `startGame` method is called which starts the game loop defined by the `_countdown` method which is called upon interval until it's stopped by the user or the allocated time runs out. On each interval of the game timer tick the `updateGame` method is called which calls private methods that update each part of the game, these include (at time of writing) the `_updateGameGiveClue` and `_updateGameChangeUnderscore` methods. Update methods in the `GameSaga` dispatch actions that are then caught by the reducers to manipulate state.

```
/**
 * @function countdown
 * Returns event channel to countdown a game
 * @param {Number} ms Milliseconds to countdown
 */
const _countdown = (ms) => {
  return eventChannel(
    emitter => {
      BackgroundTimer.runBackgroundTimer(() => {
        ms -= (COUNTDOWN_DELAY + countdownAdjustment);
        adjustCountdown(0);
        if (ms > 0) {
          emitter(ms);
          return undefined;
        }
        emitter(END);
      }, COUNTDOWN_DELAY);
      return () => stopCountdown();
    }
  );
};

/**
 * @generator _updateGameGiveClue
 * Saga generator function to give a clue on game update
 * @param {Object} game
 * @param {Number} currentTime
 */
function* _updateGameGiveClue({ game, currentTime }) {
  const { maxTimeAllowedInMs } = game;
  const timeUsedInMs = maxTimeAllowedInMs - currentTime;
  const clueToGive = find(propEq('timeToShowInMs', timeUsedInMs))(getClues(game, currentTime));
  if (clueToGive) {
    yield put(GameActions.giveClue(clueToGive));
  }
};

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
    AppSoundUtility.getInstance().replaceSoundPlaying(SOUND_UNDERSCORE_MEDIUM, SOUND_UNDERSCORE_HIGH);
    return undefined;
  }
  const timeToPlayMediumSound = maxTimeAllowedInMs / 3;
  if (timeUsedInMs >= timeToPlayMediumSound) {
    AppSoundUtility.getInstance().replaceSoundPlaying(SOUND_UNDERSCORE_LOW, SOUND_UNDERSCORE_MEDIUM);
  }
};

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
  AppSoundUtility.getInstance().play(SOUND_UNDERSCORE_LOW);
  const channel = yield call(_countdown, startTime);
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

TODO... Reducer

```
export const openGameSuccess = (state, { game }) => mergeRight(state,
  mergeRight({ ...INITIAL_STATE }, {
    selected: game,
    status: GameStatusTypes.NONE
  })
);

export const startGameSuccess = (state, { startTime }) => mergeRight(state, {
  status: GameStatusTypes.PLAYING,
  startTime
});

export const updateGameTime = (state, { currentTime }) => mergeRight(state, {
  currentTime
});

export const prepareToFinishGameSuccess = (state, { finishTime }) => mergeRight(state, {
  finishTime
});

export const finishGameSending = (state) => mergeRight(state, {
  sending: true,
  error: null
});

export const finishGameSuccess = (state) => mergeRight(state, {
  status: GameStatusTypes.FINISHED,
  sending: false,
  error: null
});

export const finishGameFailed = (state, { error }) => mergeRight(state, {
  sending: false,
  error
});

export const quitGameSuccess = (state) => mergeRight(state, {
  status: GameStatusTypes.QUIT
});

export const endGameSuccess = (state) => mergeRight(state, {
  status: GameStatusTypes.ENDED
});

export const confirmGameSending = (state) => mergeRight(state, {
  sending: true,
  error: null
});

export const confirmGameSuccess = (state) => mergeRight(state, {
  sending: false,
  error: null
});

export const confirmGameFailed = (state, { error }) => mergeRight(state, {
  sending: false,
  error
});

export const giveClue = (state, { clue }) => mergeRight(state, {
  clueToGive: clue,
  cluesGiven: mergeRight(pathOr({}, ['cluesGiven'], state), {
    [clue.id]: clue
  })
});

export const takeClueSuccess = (state, { clue }) => mergeRight(state, {
  cluesTaken: mergeRight(pathOr({}, ['cluesTaken'], state), {
    [clue.id]: clue
  })
});
```

TODO: GamePLayScreen updates to changes in state...

```
componentDidUpdate({ clueToGive: previousClueToGive, status: previousStatus }) {
  this._giveNewGameClue(previousClueToGive);
  this._showGameStatusChange(previousStatus);
}

_giveNewGameClue(previousClueToGive) {
  const HIDE_CLUE_AVAILABLE_MODAL_DELAY = 15000;
  const _openNewGameClueAvailableModal = (clue) => {
    const { openModal, closeModal, isAnyModalVisible } = this.props;
    if (isAnyModalVisible()) {
      return undefined;
    }
    openModal(ModalTypes.NEW_GAME_CLUE_AVAILABLE_MODAL_KEY, {
      clue,
      onCancelPress: this._onCancelTakeGivenClueClick,
      onConfirmPress: () => {
        closeModal(ModalTypes.NEW_GAME_CLUE_AVAILABLE_MODAL_KEY);
        setTimeout(() => this._onTakeClueClick(clue), 250);
      },
      onClosePress: this._onCancelTakeGivenClueClick
    });
    clearTimeout(this.closeClueAvailableModalTimer);
    this.closeClueAvailableModalTimer = setTimeout(
      () => closeModal(ModalTypes.NEW_GAME_CLUE_AVAILABLE_MODAL_KEY),
      HIDE_CLUE_AVAILABLE_MODAL_DELAY
    );
  };
  const { clueToGive } = this.props;
  if (clueToGive && !previousClueToGive) {
    _openNewGameClueAvailableModal(clueToGive);
    return undefined;
  }
  const previousClueToGiveId = pathOr(undefined, ['id'], previousClueToGive);
  const clueToGiveId = pathOr(undefined, ['id'], clueToGive);
  if (clueToGive && clueToGiveId !== previousClueToGiveId) {
    _openNewGameClueAvailableModal(clueToGive);
    return undefined;
  }
}

_showGameStatusChange(previousStatus) {
  const _openFailedGameModal = (game) => {
    const { openModal } = this.props;
    openModal(ModalTypes.FAILED_GAME_MODAL_KEY, {
      game,
      onAcknowledgePress: this._onAcknowledgeFailedGameClick,
      onClosePress: this._onAcknowledgeFailedGameClick
    });
  }
  const { status, game } = this.props;
  if (status === GameStatusTypes.ENDED && status !== previousStatus) {
    _openFailedGameModal(game);
    return undefined;
  }
}
```



TODO... Since development commenced on the playable experience I've been continually subscribing to research the industry more in-depth, playing games, understadning more limitations, existing tech etc etc... Also...

TODO... Mention finding the React Native game engine and how this might have saved time had I known about it

TODO... Sounds required, haptic feedback required

By looking at popular gamification apps like [Zombies Run](https://zombiesrungame.com) and reading about the psychology behind what makes a gamification app successful in various posts online such as this [Bitcatcha Post on The Psychology Of Gamification](https://www.bitcatcha.com/blog/gamify-website-increase-engagement), it's become more apparent that my app will find stickiness as a result of well executed gamification, satisfying the user's need for control, giving them an arena within which they can compete against themselves and others, establishing goals for them to aim for, giving them a sense of where they are in achieving these goals, rewarding their achievements with exclusivity and making the user feel special.





## Summary

In this post I've summarised TODO...

## References

1. [Bitcatcha Post on The Psychology Of Gamification](https://www.bitcatcha.com/blog/gamify-website-increase-engagement)
2. [Zombies Run Game Website](https://zombiesrungame.com)
