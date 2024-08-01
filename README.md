# Pig Game

This repository contains a simple dice game called "Pig Game" built with HTML, CSS, and JavaScript. The objective of the game is to be the first player to reach 100 points.

## Features

- Two-player game
- Dice roll functionality
- Turn-based gameplay
- Score tracking
- Game reset functionality

## Live Demo

Check out the live demo [here](https://qyuzet.github.io/js-pig-game).

## JavaScript Explanation

### Variable Initialization

```javascript
let scores, currentScore, activePlayer, playing;

const init = function () {
  scores = [0, 0];
  currentScore = 0;
  activePlayer = 0;
  playing = true;

  document.getElementById('score--0').textContent = 0;
  document.getElementById('score--1').textContent = 0;
  document.getElementById('current--0').textContent = 0;
  document.getElementById('current--1').textContent = 0;
  document.querySelector('.dice').classList.add('hidden');
  document.querySelector('.player--0').classList.add('player--active');
  document.querySelector('.player--1').classList.remove('player--active');
};
init();
```

- Initializes game variables.
- Sets initial scores and active player.

### Switch Player Function

```javascript
const switchPlayer = function () {
  document.getElementById(`current--${activePlayer}`).textContent = 0;
  currentScore = 0;
  activePlayer = activePlayer === 0 ? 1 : 0;
  document.querySelector('.player--0').classList.toggle('player--active');
  document.querySelector('.player--1').classList.toggle('player--active');
};
```

- Switches the active player.

### Rolling Dice Functionality

```javascript
document.querySelector('.btn--roll').addEventListener('click', function () {
  if (playing) {
    const dice = Math.trunc(Math.random() * 6) + 1;

    document.querySelector('.dice').classList.remove('hidden');
    document.querySelector('.dice').src = `dice-${dice}.png`;

    if (dice !== 1) {
      currentScore += dice;
      document.getElementById(`current--${activePlayer}`).textContent = currentScore;
    } else {
      switchPlayer();
    }
  }
});
```

- Handles dice roll.
- Updates the current score or switches player on rolling a 1.

### Holding Score Functionality

```javascript
document.querySelector('.btn--hold').addEventListener('click', function () {
  if (playing) {
    scores[activePlayer] += currentScore;
    document.getElementById(`score--${activePlayer}`).textContent = scores[activePlayer];

    if (scores[activePlayer] >= 100) {
      playing = false;
      document.querySelector('.dice').classList.add('hidden');
      document.querySelector(`.player--${activePlayer}`).classList.add('player--winner');
      document.querySelector(`.player--${activePlayer}`).classList.remove('player--active');
    } else {
      switchPlayer();
    }
  }
});
```

- Adds current score to total score.
- Checks for winning condition.
- Switches player if no winner.

### Resetting the Game

```javascript
document.querySelector('.btn--new').addEventListener('click', init);
```

- Resets the game to initial state.

## How to Run

1. Clone this repository.
2. Open `index.html` in your web browser.

## Contributing

Feel free to submit issues or pull requests for improvements and bug fixes.

## License

This project is licensed under the MIT License.
