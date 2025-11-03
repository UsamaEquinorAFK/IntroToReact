# Intro To React

### Purpose : Get started with react
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

"export" this makes the function available outside this . "default" tells other files that this is the main function in your current file. "<button>" is a JSX element. A JSX element is a combination of JavaScript code and HTML tags that describes what you’d like to display. className="square" is a button property or prop that tells CSS how to style the button. X is the text displayed inside of the button and </button> closes the JSX element to indicate that any following content shouldn’t be placed inside the button. 


``` styles.css ```
This file defines the styles for your React app. The first two CSS selectors (* and body) define the style of large parts of your app while the .square selector defines the style of any component where the className property is set to square. In your code, that would match the button from your Square component in the App.js file.


``` index.js ```
We won’t be editing this file during the tutorial but it is the bridge between the component you created in the App.js file and the web browser.

## Lets build a board 

