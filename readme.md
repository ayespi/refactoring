# Refactoring

## Learning Objectives

- Define refactoring, and give an example of something that seems like refactoring but isn't.
- Identify code "smells" indicating things that can be refactored.

## Framing

Refactoring is the process of changing existing code without changing what it does.

Today you'll be refactoring code you've already written. The code functions. It may not do exactly what you'd originally intended to do, but it functions.

**Refactoring != Fixing** 

**Challenge yourself to not change what your code does!** This will be really hard to avoid. But when you start changing the result of your code, it's a very slippery slope.

In the Industry, there will be many times when changing what the code does can break all sorts of things. Forcing yourself to stay within the scope of existing code will be important.

## Code Smells

A "code smell" is a pattern in code that allows the code to function, but is not good practice.

### Does a particular line of code repeat several times with only minor changes? 

Example: 

```js
function sayHiToAlice(){
  alert("Hi, Alice!");
}

function sayHiToBob(){
  alert("Hi, Bob!");
}

function sayHiToCarol(){
  alert("Hi, Carol!");
}

function sayHiToDavid(){
  alert("Hi, David!");
}
```

Solution: **"Extract"** these lines into their own function.

---

### Do several variable names or function names share the same word?

Example: `gameCards`, `gamePlayers`, `gameHands`, `gameScore`

Solution: The repeating word should probably be its own object.

```js
var game = {
  cards: [],
  players: [],
  hands: [],
  score: 0
}
```
---

### Is a particular method/function over 10 lines long?

Example:

```js
function dealCards(){
  deck.sort(function(a, b){
    if(Math.random() < 5) return -1;
    else return 1;
  });
  players.forEach(function(player){
    player.hand = deck.pop();
  });
}
```

Solution: Break it up into several smaller methods/functions... maybe! This isn't always appropriate, but is a good "rule of thumb" to maintain. Functions even just over 5 lines can be very difficult to read. Identify which different processes take place in your function, and extract each into its own function.

```js
function shuffle(){
  deck.sort(function(a, b){
    if(Math.random() < 5) return -1;
    else return 1;
  });
}
function deal(){
  players.forEach(function(player){
    player.hand = deck.pop();
  });
}
```

---

### Do you have multiple global variables and functions?

Example:

```js
var users;
var data;
var views;
function renderData(){

}
```

Solution: Create one global variable -- an object -- and attach everything to it.

```js
var app = {
  users: [],
  data: [],
  views: [],
  renderData: function(){

  }
}
```

Global variables are never *garbage-collected*. This means they can seriously slow down your app.

---

### Does it take you more than 3 seconds to understand what a variable or method is doing?

Example:

```js
alert("Here's a really important piece of information: " + myvariable);
```

Solution: Name it something better! There's not really any downside to giving variables and functions longer names if necessary

```js
alert("Here's a really important piece of information: " + secretMessageFromPresident);
```

---

### Is your file more than 100 lines long?

Solution: Split it into several files, each concerned with a specific part of the code.

---

### Do you find yourself having to count parentheses and braces to find the matching paren or brace?

Example:

```js
$(document).ready(function(){ var game = {
  title: "Checkers", players: []
    }function playGame()
{
  alert("You're playing checkers!");
}
}
)
```

Solution: Indent your code, and keep things consistent! In Atom, if you "Select All" (Command + A) and go to Edit > Lines > Autoindent, it pretties everything up for you.

