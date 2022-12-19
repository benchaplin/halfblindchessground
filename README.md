# halfblindchessground 

Fork of [https://github.com/lichess-org/chessground](https://github.com/lichess-org/chessground).

## Installation

To install the stable version:

```
# npm
npm install halfblindchessground

# yarn
yarn add halfblindchessground
```

## Usage

There is a piece of new [config](https://github.com/benchaplin/halfblindchessground/tree/master/src/config.ts)/[state](https://github.com/benchaplin/halfblindchessground/tree/master/src/state.ts):

```js
halfBlindMove?: HalfBlindMove | number; // half-blind move on the board or number of moves until the next
```

This state must be controlled by the user in the `events.after` function, like so:

```js
function afterExample(orig, dest) {
  const move = halfBlindChess.move({ from: orig, to: dest });
  cg.set({
    halfBlindMove: move.halfBlind
      ? move
      : typeof cg.state.halfBlindMove === "number"
        ? cg.state.halfBlindMove - 1
        : 1
  });
  // ...
}
```

Half-blind pieces are marked with opacity.