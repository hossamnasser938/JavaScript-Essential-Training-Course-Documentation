# Typing speed tester project

This project aims to build a typing speed tester in which there is some text for you to type and a counter starts counting as soon as you start typing. I have also added an error counter which counts how many errors you have made during typing.

* A **CSS** tip: to change how a button looks like when the mouse hovers over, you need to access this button and then use the hover property and add the new looking. Suppose that your button has an id `reset`:
```js
#reset {
  padding: .5em 1em;
  font-size: 1.2em;
  font-weight: bold;
  color : orange;
  background-color : white;
  border : 10px solid orange;
}
#reset: hover {
  color : white;
  background-color : orange;
}
```
In this CSS sheet the rules under `reset` are applied to the button when you are not hovering over. Once you hover over the button, the rules under `reset : hover` are applied. Interchanging the colors of the text and the background, as you see in this example, makes the button looks great.

* To detect when a user start typing in some area, use either the event `keypress` or the event `keyup` both of them fire as soon as a user hits a key on the keyboard but there is a little difference between them:
    * `keypress` fires when keys that produce character value(numeric, alphabetic, and punctuation keys) is **pressed** which means it fires **right before** the key typed is captured so when accessing the text typed, it **does not** contain the key typed. Unfortunately, this event is now **deprecated** and it is recommended to use either `keydown`(fires when **any key** is **pressed**) or `beforeinput`(fires when an input DOM element_such as `<input>`, `<select>`, `<textarea>`_ is about to be modified).
    * `keyup` fires when any key(not just keys that produce character value) is **released** which means it fires **right after** the key(if it is a key that produce character value) typed is captured(when a key is released) so when accessing the text typed it **does  contain** the key typed.

* To access the text entered by the user in a `<textarea>` element, suppose that we have a textarea DOM element with id testarea. We need first to get a reference to that element and then access the `value` property:
```js
const TEST_AREA = document.querySelector("#testarea");
var textEntered = TEST_AREA.value;
```
to get the length of that text access the `length` property:
```js
var textEnteredLength = TEST_AREA.value.length;
```

* To make a timer, we can make good use of the `setInterval` methood presented in lesson 5. Suppose that we wanna build a timer in this form **minutes:seconds:moment** where a moment is hundredths of a second. we can declare a global `counter` initialized with zero and each 10 milliseconds(hundredths of a second) we increment it and then take this counter and do some math to calculate the parts of the timer. We start the timer with first character typed by the user:
```js
/* THE_TIMER is a reference to the DOM element of the timer */
const THE_TIMER = document.querySelector(".timer");
var counter = 0; // Global counter
var minutes, seconds, hundredths;
var interval;
function startTimer() {
  let textEnteredLength = TEST_AREA.value.length;
  if(textEnteredLength == 0) {
    interval = setInterval(runTimer, 10);
  }
}
function runTimer() {
  counter++;
  minutes = Math.floor((counter / 100) / 60)
  seconds = Math.floor(counter / 100) - minutes * 60;
  hundredths = counter % 100;
  THE_TIMER.innerHTML = minutes + ":" + seconds + ":" + hundredths;
}
TEST_AREA.addEventListener("keypress", startTimer, false);
```
Hint: `Math.floor` function gets the integer value of a floating-point value.
* Any time we wanna stop the counter, we just clear the interval, and clear the counter variable(to start with the zero the next time).
```js
function stopCounter() {
  clearInterval(interval);
  counter = 0;
}
```  

* We can enhance how the timer looks. We want the timer to display two-digit numbers even if one-digit number exists so instead of "0:8:65" we want "00:08:65". We can declare a helper function that leads a zero if the number given is one-digit. We can do that with no care about strings and integers because we know that whenever a number stored as a string JavaScript treats it as a number whenever we attempt to use it as a number.
```js
function leadZero(n){
  if(n <= 9) {
    n = "0" + n;
  }
  return n;
}
```
* Now we can modify how we output the timer using the `leadZero` function.
```js
THE_TIMER.innerHTML = leadZero(minutes) + ":" + leadZero(seconds) + ":" + leadZero(hundredths);
```

* To facilitate the typing process we now support the typist with a spell check functionality to help him recognize earlier when he makes an error. So we wanna compare what the user typed with the original text each time he types a letter and then change the color of the border of test area with different colors in three situation:
    1. user has typed a letter correctly.
    2. user has typed a letter wrongly.
    3. user has finished typing the whole text correctly.
```js
/* the original text that the user should type */
const ORIGINAL_TEXT = document.querySelector("#origin-text p").innerHTML;
/* the area where the TEST_AREA exists */
const TEST_WRAPPER = document.querySelector(".test-wrapper");
function spellCheck() {
  var textEntered = TEST_AREA.value;
  var matchedOriginalText = ORIGINAL_TEXT.substring(0, textEntered.length);
  if (textEntered === ORIGINAL_TEXT) {
    // situation 3: the user has finished typing the whole text correctly
    stopCounter();
    TEST_WRAPPER.style.borderColor = "green";
  } else {
    if (textEntered === matchedOriginalText) {
      // situation 1: the user has typed a letter correctly
      TEST_WRAPPER.style.borderColor = "blue";
    } else {
      // situation 2: the user has typed a letter wrongly
      TEST_WRAPPER.style.borderColor = "red";
    }
  }
}
TEST_AREA.addEventListener("keyup", spellCheck, false);
```   
Hint: `substring` is a function that gets a portion of a string(substring). It takes as arguments: the index of the character to start from and the ((index of the character to end at) + 1). If `substring` is given one parameter it returns the substring that starts with the character with index specified by this parameter till the end of the string. 

* Now we wanna count the number of errors the user has made during typing. It is very simple. We declare a global variable `errorsCounter` initialized with zero and whenever we detect an error we increment it. We modify this block:
```js
else {
  // situation 2: the user has typed a letter wrongly
  TEST_WRAPPER.style.borderColor = "red";
}
```
to be:
```js
else {
  // situation 2: the user has typed a letter wrongly
  TEST_WRAPPER.style.borderColor = "red";
  ERRORS_FIELD.innerHTML = ++errorsCounter;
  /* ERRORS_FIELD is the DOM that displays the errors count */
}
```  
