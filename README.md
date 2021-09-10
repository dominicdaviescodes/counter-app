# counter-app

go see it live! https://ddcodes-counter-app.netlify.app/

## version 1
* Click Add for counter to go up
* Click Subtract for counter to go down
* Click reset for counter to go to zero
* fontawesome icons

Here's the logic in v1.

```js
const count = document.querySelector(".count")
const add = document.querySelector(".add")
const resetCount = document.querySelector(".reset")
const sub = document.querySelector(".subtract")

add.addEventListener("click", () => {
  count.innerHTML++
})

resetCount.addEventListener("click", () => {
  count.innerHTML = 0
})

sub.addEventListener("click", () => {
  count.innerHTML--
})
```
## version 2 - Event delegation
there is a better way instead of adding multiple EventListener's. 

Event delegation: we can add a single EventListener on the parent of the 3 buttons.  Parent is div 'buttons'.  From there we can individually target the btn's.

We pass an event in as a param. 
Then we use a conditional so we can know which event to trigger.

Event delegation: we can add a single EventListener on the parent of the 3 buttons.  Parent is div 'buttons'.  From there we can individually target the btn's.

So instead of 3 EventListener's we have just the one on the parent. We also don't need to access those buttons in the DOM using variables.

#### Button issue
I did have a few issues clicking the buttons and the value not changing.

The fix involved adding each button's class to the font awesome icon's classes. Now the buttons work fine.

Here's the logic, not sure about all the if's?

```js
const buttons = document.querySelector(".buttons")

buttons.addEventListener("click", (e) => {
  // console.log("inside")
  if (e.target.classList.contains("add")) {
    count.innerHTML++
  }
  if (e.target.classList.contains("subtract")) {
    count.innerHTML--
  }
  if (e.target.classList.contains("reset")) {
    count.innerHTML = 0
  }
})
```

## version 3: the color thing
* negative numbers are red
* positive numbers are yellow
* reset/zero is white

We create a function setColor() to set the color for all 3 states (add, subtract and reset)

```js
function setColor() {
  if (count.innerHTML > 0) {
    count.style.color = "yellow"
  } else if (count.innerHTML < 0) {
    count.style.color = "orangered"
  } else {
    count.style.color = "white"
  }
}
```
We then call setColor() when each event fires(when each button is clicked)

```js
buttons.addEventListener("click", (e) => {
  // console.log("inside")
  if (e.target.classList.contains("add")) {
    count.innerHTML++
    setColor()
  }
  if (e.target.classList.contains("subtract")) {
    count.innerHTML--
    setColor()
  }
  if (e.target.classList.contains("reset")) {
    count.innerHTML = 0
    setColor()
  }
})
```