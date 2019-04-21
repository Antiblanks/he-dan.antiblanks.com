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

TODO... This is the experience how it stands today... Iteratively improved etc etc...

TODO... Introducing narrative into the experience touched on in this [post]({% post_url 2019-03-01-week-5-concept-art %}) + other improvements, include play game research?...

TODO... Each flow image here + description...

### Technical elements within the experience

TODO... Game state

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

TODO... Game loop

```
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

By looking at popular gamification apps like [Zombies Run](https://zombiesrungame.com) and reading about the psychology behind what makes a gamification app successful in various posts online such as this [Bitcatcha Post on The Psychology Of Gamification](https://www.bitcatcha.com/blog/gamify-website-increase-engagement), it's become more apparent that my app will find stickiness as a result of well executed gamification, satisfying the user's need for control, giving them an arena within which they can compete against themselves and others, establishing goals for them to aim for, giving them a sense of where they are in achieving these goals, rewarding their achievements with exclusivity and making the user feel special.





## Summary

In this post I've summarised TODO...

## References

1. [Bitcatcha Post on The Psychology Of Gamification](https://www.bitcatcha.com/blog/gamify-website-increase-engagement)
2. [Zombies Run Game Website](https://zombiesrungame.com)
