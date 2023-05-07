## useState
useState is a hook which force the react to rerender the function.
useState is a React Hook that lets you add a state variable to your component.

## what are hooks?
hooks are external function which is cannot be done in side a compnonent but are forces the ui compnent to do some thing.

import {useState} from react;\
const [counter,setCounter]=useState(0);


## what will be output of this code
```
import {useState} from react;
function counter(){
const [counter,setCounter]=useState(0);
function handleClick(){
setCounter(counter+1);//outpout:"0+1"
setCounter(counter+1);//outpout:"0+1"
setCounter(counter+1);//outpout:"0+1"
console.log(conter+" counter");
}
return(
 <h1>{counter}</h1>
 <button onClick={handleClick}>Add</button>
)
}
```
setCounter will not immediately rerender the function first all the setstate are queued and  evaluated .than rerender  is called .

## what will be output of this code
```
import {useState} from react;
function counter(){
const [counter,setCounter]=useState(0);
function handleClick(){
setCounter(counter=>counter+1);//outpout:"0+1"
setCounter(counter=>counter+1);//outpout:"1+1"
setCounter(counter=>counter+1);//outpout:"2+1"
console.log(conter+" counter");
}
return(
 <h1>{counter}</h1>
 <button onClick={handleClick}>Add</button>
)
}
```
setCounter will not immediately rerender the function first all the setstate are queued and  evaluated .than rerender  is called but updater function updates the value of 
counter.

## Caveats 
1. The set function only updates the state variable for the next render. If you read the state variable after calling the set function, 
you will still get the **old value** that was on the screen before your call.

2. If the new value you provide is **identical** to the current state, as determined by an **Object.is** comparison, React will **skip re-rendering** 
the component and its children. This is an optimization. Although in some cases React may still need to call your component before skipping the children, 
it shouldn’t affect your code.

3. React **batches state updates**. It updates the screen after all the event handlers have run and have called their set functions.
 This prevents multiple re-renders during a single event. In the rare case that you need to force React to update the screen earlier, 
 for example to access the DOM, you can use **flushSync**.

4. Calling the set function during rendering is only allowed from within the currently rendering component.
React will discard its output and immediately attempt to render it again with the new state. 
This pattern is rarely needed, but you can use it to store information from the previous renders. See an example below.
 
5. In Strict Mode, React will call your updater function twice in order to help you find accidental impurities.
This is development-only behavior and does not affect production. If your updater function is pure (as it should be),
 this should not affect the behavior. The result from one of the calls will be ignored.

