# Intro To React

### Purpose : Getting started with react if you are a complete beginner
### How ? : We build a game
### Why ? : Well because its fun

A super similar tutorial can be followed [here](https://react.dev/learn/tutorial-tic-tac-toe) but we want to develop locally so we will just clone this repo. The link is also very helpful so I recommend you give it a read. 

## Setup for tutorial

1 - Install [Node.js](https://nodejs.org/en/download).

2 - Clone this repository.

3 - Run ``` npm install``` to install dependencies defined in package.json.

4 - Run ``` npm start``` to start a local server. 

## Overview of what we have so far

``` App.js ```

In this file we are making a component. In React, a component is a piece of reusable code that represents a part of a user interface. Components are used to render, manage, and update the UI elements in an application. Lets look at this line by line.

``` java 
export default function Square() {
  return <button className="square">X</button>;
}
```

"export" this makes the function available outside this . 

"default" tells other files that this is the main function in your current file. 

"<" "button" ">" is a JSX element. A JSX element is a combination of JavaScript code and HTML tags that describes what you’d like to display. 

className="square" is a button property or prop that tells CSS how to style the button. X is the text displayed inside of the button and </button> closes the JSX element to indicate that any following content shouldn’t be placed inside the button. 


``` styles.css ```

This file defines the styles for your React app. The first two CSS selectors (* and body) define the style of large parts of your app while the .square selector defines the style of any component where the className property is set to square. In your code, that would match the button from your Square component in the App.js file.


``` index.js ```

We won’t be editing this file during the tutorial but it is the bridge between the component you created in the App.js file and the web browser.

## Lets build a board 

Lets start by adding more squares 


``` java
export default function Square() {
  return <button className="square">X</button><button className="square">X</button>;
}

``` 


This will raise an error and react will ask whether we want to use react fragments. React components need to return a single JSX element and not multiple adjacent JSX elements like two buttons. To fix this we can do something like this 


``` java
export default function Square() {
  return (
    <>
      <button className="square">X</button>
      <button className="square">X</button>
    </>
  );
}

```

Sweet we have our two buttons, lets repeat this 9 times and see what happens. 

"Ehhh" is probably the reaction you have since now you have 9 buttons in a line which doesnt looks anything likes tic tac toe board. Lets fix that by defining rows and using another .css style element called board-row. The board-element contains rules such that each board row expands upon adding more squares without causing overlaps or overflow issues. 

``` java
export default function Square() {
  return (
    <>
      <div className="board-row">
        <button className="square">1</button>
        <button className="square">2</button>
        <button className="square">3</button>
      </div>
      <div className="board-row">
        <button className="square">4</button>
        <button className="square">5</button>
        <button className="square">6</button>
      </div>
      <div className="board-row">
        <button className="square">7</button>
        <button className="square">8</button>
        <button className="square">9</button>
      </div>
    </>
  );
}

```

Can you guess a small issue in the Square component above ? Well, its not really a square anymore is it so we can rename it Board in our code. Making the component looks something like this, 

``` java
export default function Board() {
  //...
}

```

## Well we have board but not a game yet, lets make the squares take in some form of input

React components allows you to define smaller reusable components to avoid messy code. ( and maybe this is what the fancy folks call "Refactoring?" ). Lets look at the code block below.  


``` java

function Square() {
  return <button className="square">1</button>;
}

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}

```

We created a function, which is not the main function of this file, and it wont be export out of this file, it is merely used to simplify Board component. 

Problem ? We have nine 1s. Now there is nothing wrong with 1s but we have lost the 1-9 numbered list that we had. 

Fix ? We will learn to use props to pass down values into components, look at the code block below 

``` java

function Square({ value }) {
  return <button className="square">value</button>;
}

```

```function Square({ value })``` indicates the Square component can be passed a prop called value. 

Hahah not exactly what we wanted, now we have value printed 9 times in the board. 

You wanted to render the JavaScript variable called value from your component, not the word “value”. To “escape into JavaScript” from JSX, you need curly braces. Add curly braces around value in JSX like so:

``` javascript

function Square({ value }) {
  return <button className="square">{value}</button>;
}


export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square value="1" />
        <Square value="2" />
        <Square value="3" />
      </div>
      <div className="board-row">
        <Square value="4" />
        <Square value="5" />
        <Square value="6" />
      </div>
      <div className="board-row">
        <Square value="7" />
        <Square value="8" />
        <Square value="9" />
      </div>
    </>
  );
}


```

Nice! We have our numbers back. 


## Lets make the component interactive

Let’s fill the Square component with an X when you click it. Declare a function called handleClick inside of the Square. Then, add onClick to the props of the button JSX element returned from the Square:

``` java

function Square({ value }) {
  function handleClick() {
    console.log('clicked!');
  }

  return (
    <button
      className="square"
      onClick={handleClick}
    >
      {value}
    </button>
  );
}

```

If you click on a square now, you should see a log saying "clicked!" in the Console tab. (Right click and select Inspect in the browser)

Clicking the square more than once will log "clicked!" again. Repeated console logs with the same message will not create more lines in the console. Instead, you will see an incrementing counter next to your first "clicked!" log.

As a next step, we want the Square component to “remember” that it got clicked, and fill it with an “X” mark. To “remember” things, components use state.

React provides a special function called useState that you can call from your component to let it “remember” things. Let’s store the current value of the Square in state, and change it when the Square is clicked.

Import useState at the top of the file. Remove the value prop from the Square component. Instead, add a new line at the start of the Square that calls useState. Have it return a state variable called value:

``` java

import { useState } from 'react';

function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    //...

```

value stores the value and setValue is a function that can be used to change the value. The null passed to useState is used as the initial value for this state variable, so value here starts off equal to null.

Since the Square component no longer accepts props anymore, we’ll remove the value prop from all nine of the Square components created by the Board component.

``` java

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}

```

Also we can update the handleClick function to update the state

``` java

function handleClick() {
    setValue('X');
  }

```

After all this the App.js should look like this 

``` java

import { useState } from 'react';

function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    setValue('X');
  }

  return (
    <button
      className="square"
      onClick={handleClick}
    >
      {value}
    </button>
  );
}

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}

```

## React Developer tools



## Finish the game




