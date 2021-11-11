# React for Vue 2 Devs

Hey there! This is a guide for developers with Vue 2 experience, who might be interested in learning React. I will structure this document in a way that will allow a Vue developer to find the tools they need to accomplish what they already know, but in React.

# But why?

I know, this seems crazy... But we recently have adopted a new team at my work and their tech stack includes React. I've recently React after using Vue for a long while, and after drawing the parallels between modern React and Vue, I believe sharing some of my learning experience could be of benefit to any other developer in this position.

## Vue Lifecycle Hooks... But in React!

As a Vue developer, you should know some of these lifecycle hooks. I'm going to explain how you can do a **mounted** hook, and a **updated** hook, but in React.

### Mounted
In React, your `mounted()` hook will be using the `useEffect` hook from React's library of hooks. `useEffect` takes two parameters, an anonymous function returning what you would like to happen, and an array of dependencies. We just want this to emulate an on mount behavior, so we will give it an empty array. `fetchData()` will fire on mount, or more accurately in React, the first render of your component.
```
import { useEffect } from "react"

useEffect(() => {
  fetchData()
}, [])
```
What happens if we completely omit the second dependencies array parameter entirely? Well that brings us to our next lifecycle hook. 

### Updated
While a bit more rare of a use case, maybe you'd like to fire off an action every time the component is updated, or rather in React, the component re renders.
```
import { useEffect } from "react"

useEffect(() => {
  doSomething()
})
```
The example above demonstrates how you would accomplish a `updated()` hook from Vue, but in React!

https://reactjs.org/docs/hooks-effect.html

But what if we bring that dependency array, and throw some stuff in there...? 
## Watchers

In Vue, when we want a side effect after something has changed, we would reach for a watcher. To do this in React, we're going to go ahead and whip out another `useEffect` hook. It's going to look like this...

```
import { useEffect } from "react"

useEffect(() => {
  doSomething()
}, [thingToWatch, otherThing])
```
Load up the dependencies array with the things you want to watch, and in the first function param, do what you need to do.

## Methods and Computed Properties

Methods in Vue are essentially functions that take params, and does an action. Sometimes it returns a value, sometimes it just does a side effect like changing state, whatever you need really. Methods in React are just functions. Computed properties would also just be plain ol' functions as well!
```
function add(n1, n2) {
  return n1 + n2
}
```
**Note:** If you really need the performance optimization, to achieve the caching functionality closer to something like a Vue computed property, take a look at React hook `useMemo` .
https://reactjs.org/docs/hooks-reference.html#usememo

## Reactive state, in React - Or the data function in Vue
We all know this guy here:
```
data() {
  return { count: 0 }
}
```
But what is the React equivalent?

React is very small and out of the way, you can create variables and change them with vanilla JavaScript, but you might find that in your template, some values might not actually reactively update even though you've changed them. Similar to holding state in your Vue's data function return, you'll need to declare what your state will be in React. For managing state in React we will need to use the `useState` hook.


```
import React, { useState } from "react"

function Example() {
 const [count, setCount] = useState(0)
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  )
}
```
In this example we employ an array destructuring  assignment, to create a getter and a setter for our `count` state. I lifted this directly from the docs, if this isn't clear enough go read them!
https://reactjs.org/docs/hooks-state.html

# What about templating?

React components usually return JSX, which is some sort of HTML in JavaScript magic. You can leverage the full power of JavaScript within these "templates". Really, you can assign a piece of UI to a variable, return it from a function, introduce JavaScript logic. Things like `v-for` and `v-if` are basic array maps and filters, or conditional operators respectively.

Check it out:
https://reactjs.org/docs/introducing-jsx.html

# Where to go from here?

Maybe you need something like **Vuex** for state management. React has a hook for that called `useContext`. 
https://reactjs.org/docs/hooks-reference.html#usecontext
https://kentcdodds.com/blog/how-to-use-react-context-effectively

Pairing this with the `useReducer` hook, you could be `dispatch`ing actions to manage your state. It all seems so familiar...
