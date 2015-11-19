# list-diff [![build](https://circleci.com/gh/livoras/list-diff/tree/master.png?style=shield)](https://circleci.com/gh/livoras/list-diff) [![codecov.io](https://codecov.io/github/livoras/list-diff/coverage.svg?branch=master)](https://codecov.io/github/livoras/list-diff?branch=master)

Diff two lists in time O(n). 

The algorithm finding the minimal amount of moves is [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance) which is O(N*M). This algorithm is not the best but is enougth for front-end DOM list manipulation and is mostly influenced by [virtual-dom](https://github.com/Matt-Esch/virtual-dom/blob/master/vtree/diff.js) algorithm.

### Install

    $ npm install list-diff

### Usage

```javascript

    var diff = require("list-diff")
    var oldList = [{id: "a"}, {id: "b"}, {id: "c"}, {id: "d"}, {id: "e"}]
    var newList = [{id: "c"}, {id: "a"}, {id: "b"}, {id: "e"}, {id: "f"}]

    var moves = diff(oldList, newList, "id")
    // `moves` is a sequence of actions (remove or insert): 
    // type 0 is removing, type 1 is inserting
    // moves: [
    //   {index: 3, type: 0},
    //   {index: 0, type: 1, item: {id: "c"}, 
    //   {index: 0, type: 0}, 
    //   {index: 4, type: 1, item: {id: "f"}}
    // ]

    moves.forEach(function(move) {
      if (move.type === 0) {
        oldList.splice(move.index, 1) // type 0 is removing
      } else {
        oldList.splice(move.index, 0, move.item) // type 1 is inserting
      }
    })

    // now `oldList` is equal to `newList`
    // [{id: "c"}, {id: "a"}, {id: "b"}, {id: "e"}, {id: "f"}]
    console.log(oldList) 

```

### License 
MIT



