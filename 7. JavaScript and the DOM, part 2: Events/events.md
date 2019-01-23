## What are DOM events?
* Everything that happens in the browser is an **event**, for example:
    * Opening the browser.
    * Typing a URL and hitting enter.
    * Clicking a link.
    * Moving the mouse.  
All of these are events.
* Whatever you do in the browser you simply **fire events** and the browser responds to these events using preconfigured responses.
* Using JavaScript, we can write scripts that are executed whenever the browser captures specific events.
* UP until now what we do is write scripts that run as soon as the HTML document loads or write scripts directly on the console. However, that does not add any interactivity to our web pages(**passive form**). To add such **interactivity**, we use events(functions triggered whenever specific interactions occurr).
* The way we **handle events** in JavaScript is as follows:
    1. identify the **DOM node**(element) that the interactivity will occurr above.
    2. identify the **event** that you want to capture and bind that event to the element.
    3. Define the **function** that will be triggered when this event occurrs.

## Some typical DOM events
* Events can be categorized into:
    * **Browser-level events**  
Events that are related to the browser itself such as: loading the document, window sizing, etc.
    * **DOM-level events**  
Events that are related to a specif DOM node such as clicking on a node, focusing a node, hitting submit button, etc.
* Some common **Browser-level** events:
    * ` Load ` tells that the resource and its dependents have finished loading.
    * ` Error ` tells that the resource has failed to load.
    * ` Online `
    * ` Offline `
    * ` Resize ` tells that the view has been resized.
    * ` Scrool ` tells that the view has been scrolled up, down(vertically), left, or right(horizontally).
* Some common **DOM-level** events:
    * ` Focus ` tells that a specific element has been given focus by touching, clicking, etc.
    * ` Blur ` tells that a specific element has lost focusing(for example leaving from one field to another in a form).
    * ` Reset ` form-specific event: tells that a reset button has been clicked.
    * ` Submit ` form-specific event: tells that submit button has been clicked.
    * **Mouse events** including ` Click `, ` Mouseover `, ` Drag `, ` Drop `, etc.
* There are other **custom events**:
    * **Media events**: related to audio and video playback.
    * **Progress events**: related to progress on the browser.
    * **CSS transition events**: when transition starts/runs/ends etc.
* **Hint**: Any event the browser can react to, you can capture and bind it with your own script triggered whenever the event fires.

## Trigger functions with event handlers
* Let's see our first example to catch an event whenever it fires and handle it.
* Our event in this example will be clicking a button.
* The logic goes as follows:
    1. identify the element(button) on which the event will fire.
```
const BOOK_NOW_BTN = document.querySelector(".cta a");  // class
```
    2. identfy the event to capture. Our event in this example is clicking the button. Each element comes with an **event handler** to handle clicking it which is ` onclick `.
    3. define the function to be triggered when the button is clicked. Here we want to just show/hide an alert when clicking the button.
```
const ALERT = document.querySelector("#alert"); // id
function reveal(){
  ALERT.classList.toggle("hide");  
  /* here we just enable/disable a class called hide which hides the alert section */
}
```
    4. Connect all of the element, event handler, and the function to be triggered.
```
BOOK_NOW_BTN.onclick = reveal;
```
* What if an event has a default behaviour carried out by the browser even if you define a custom handler for it, and you want to get rid of that default behaviour?  
Simply, the function that you bind with the event is given as argument an instance of the event so you can use that object to stop the default behaviour.
```
function reveal(e){
  e.preventDefault();
  /* Here we stopped the default behaviour of the event */
  ALERT.classList.toggle("hide");
}
```

## Add and use event listeners
* What if we wanna do multiple things(functions) when a single event fires? What first comes to mind is simply bind multiple functions with the event handler like that:
```
BOOK_NOW_BTN.onclick = reveal;
BOOK_NOW_BTN.onclick = function(){ console.log("The button was clicked!"); };
/* Good use case for anonymous function tied with an event(No need to give it a name) */
```
Actually this does not work as expected. The second function(the anonymous one) will override ` reveal ` function and just the anonymous function will get executed on firing the event.
* Alternatively, we can use **event listeners**. An event listener is something that observes a specific event and once it fires it executes a preconfigured function. In that way we can define multiple event listeners for a single event all of which performs indepenedently.
```
BOOK_NOW_BTN.addEventListener("click", reveal, false);
BOOK_NOW_BTN.addEventListener("click", function(){ console.log("The button was clicked!"); }, false);
```
* Some useful things from the **mouse-tracker demo**:
    * How to draw a circle in an HTML document?
        1. in HTML:
```
<div class="circle"></div>
```
        2. in CSS:
```
.class{
  position : absolute; <!-- to be free to move -->
  width : 50px;
  height : 50px;
  <!-- width and height attributes define the radius of the circle. They must be the same -->
  color : transparent; <!-- color inside the div -->
  border: 2px solid red;
  border-radius : 50%; <!-- this attribute is what makes the div circle. If we removed it the result is a square. Actually it could be any value from 50% to 100% -->
}
```

    * How to get the dimensions of the browser window?
```
var windowWidth = window.innerWidth;
var windowHeight = window.innerHeight;
```
    * How to get the position of the mouse pointer?
```
const BODY = document.body;
function mouseCoordinates(e){
  mouseX = e.clientX;
  /* clientX attribute gets the distance from the left most of the window to the mouse pointer */
  mouseY = e.clientY;
  /* clientY attribute gets the distance from the top most of the window to the mouse pointer */
}
BODY.addEventListener("mousemove", mouseCoordinates, false;)
/* The mousemove event fires whenever the mouse move on the area of the body */  
```
    * To move the circle as the mouse moves? Add this code to the function ` mouseCoordinates `.
```
const CIRCLE = document.queySelector(".circle");
CIRCLE.style.left = mouseX;
CIRCLE.style.top = mouseY;
```
    * To do something when the mouse enters an element or leave it use the events ` mouseenter `, ` mouseleave ` respectively.
```
CIRCLE.addEventListener("mouseenter", function(){ /* Do something */ }, false);
CIRCLE.addEventListener("mouseleave", function(){ /* Do something */ }, false);
```

## Pass arguments via event listeners
* What is if we wanna pass arguments to a to-be-triggered function for an event? The reason why we can not do it by just the normal way is that if we do it the normal way like this:
```
BOOK_NOW_BTN.addEventListener("click", reveal(x), false);
```
the function will get called as soon as the browser encounters it. That is not what we want. We just wanna register the function with the event.
* Alternatively, we can pass arguments by wrapping the ` reveal ` function in an outer ` anonymous function `(That is another useful use case for the anonymous function).
```
BOOK_NOW_BTN.addEventListener("click", function(){ reveal(x); }, false);
```
* Sometimes we wanna pass the object that caused the event to the to-be-triggered function. We can do that by simply pass ` this ` to the function.
```
BOOK_NOW_BTN.addEventListener("click", function(){ reveal(this); }, false);
```
now we can access this object inside the function.
```
function reveal(c){
  e.preventDefault();
  c.innerHTML = "Hi!";
  ALERT.classList.toggle("hide");
}
```
Unfortunately, this will generate an error. The ` reveal ` function now know nothing about ` e `(the instance of the event). We wanna pass it to the ` reveal ` function. The problem is that ` e ` is not accessible **within** the anonymous function. Instead it is only accessible before entering the anonymous function so the only way to pass ` e ` is to pass it to the anonymous function first.
```
BOOK_NOW_BTN.addEventListener("click", function(e){ reveal(e, this); }, false);
```
Now the function ` reveal ` accepts two arguments.
```
function reveal(e, c){
  e.preventDefault();
  c.innerHTML = "Hi!";
  ALERT.classList.toggle("hide");
}
```

## Chapter quiz
1. When does a browser event fire?  
On user, script, or browser interaction
2. Using event handlers you can trigger several different functions using a single event?  
FALSE
3. An event listener listens is triggered the first time an event takes place?  
FALSE
4. Arguments can be passed to a function triggered by an event listener?  
TRUE
