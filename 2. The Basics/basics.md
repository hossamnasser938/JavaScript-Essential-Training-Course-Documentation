## Tools for JavaScript development
JavaScript needs no compilation to run on the browser. This means what tools you need are:
- TextEditor.
- Browser.

## Introducing the browser console
* We can write and execute JavaScript code directly in the browser using the **console**.
    1. Hit right click on the browser
    2. select inspect
    3. choose console
  
* First lines of JavaScript:  
    * Alert command shows a pop up with information in the quotes.  
``` 
alert("Hello world") 
```
    * Let's declare a variable to store the date and then alert it  
```
var date = new Date()
alert("Today is " + date)
```
    * Instead of poping information on the browser using ` alert ` we can log it on the console for debugging purpose.
```
console.log("Today is " + date)
```
    * We can change the elements in the HTML document using JavaScript.
```
document.body.innerHTML = "<h1> Today is " + date + "</h1>"
```

## Add inline JavaScript to an HTML
* In a real project we do not write and execute JavaScript from the console but we have two choices:
    * Write JS inside the HTML document.
    * Write JS in a separate file and connect it with the HTML document telling the browser to download this file alngside the HTML document.
* To write JS inside the HTML document, we add a special tag called ` script `.
* The place of the ` script ` tag depends on **when** you want the script to be executed and other factors.
    * If we want the ` script ` to run **before** the HTML elements are rendered, we can add it within the ` head ` element.
    * If we want the ` script ` to run **after** the HTML elements are rendered, we can add it after the ` body ` element.
* Be careful when you put the ` script ` tag before the body. In this case you can not do something like this:
```
document.body.innerHTML = "</h1> Hello world </h1>";
```
This will immediately generate this error: ` Cannot set property 'innerHTML' of null `  
As the body element has not yet been rendered. It is currently(at the time the script is being executed) null since the browser interprets the document from top to down.

## Add JavaScript in an external file
* For JS code that affects more than one page it is better to put it in a separate file and whenever you need to include in an HTML document, simply reference it in the HTML document the same we do with external assets lik CSS files.
    1. Create a file for the script with .js extension.
    2. reference the file in the ` script ` tag within the HTML document using the ` src ` attribute.
```
<script src = "script.js"></script>
```

* Anytime the browser parses an HTML document and encounters a JS file reference it goes, downloads it, and then proceed with the rest of the HTML document. This may slow down the performance of the site significantly. This problem is called **JavaScript render blocking**.
* Hint: if the JS files are referenced in the ` header ` the **JavaScript render blocking** will exist but it will take less time. So it is best practice to reference JS files at the bottom after the ` body ` tag.
* To solve this problem, we have choices:
    * Download the JS file **asyncronously** while parsing the HTML document and in this situation the **JavaScript render blocking** will exist only in the time of executing the JS file. This happens by adding the ` async ` attribute to the ` script ` tag.
```
<script src = "script.js" async></script>
``` 
    * Download the JS file when everything else is loaded(postpone or defer its downloading) even if it is referenced in the ` header ` . This happens by adding the ` defer ` attribute in the ` script ` tag.
```
<script src = "script.js" defer></script>
```

## How to write JavaScript: A crash course
Some rules for writing JavaScript:
* JavaScript is case sensitive.
* Use **camelCase** as naming convention.
    * A variable or a function starts with a lowercase letter.
    * A class or object starts with an uppercase letter.
    * A constant consists of all_caps letters.
* Whitespaces do not matter for the parser but do for humans.
* End each statement with a semicolon just for readability. JavaScript does noy need semicolons.
* Use comments liberally(most frequently).

## Chapter Quiz
1. Code entered in the browser console is saved to the current document?  
FALSE.
2. Inline JavaScript runs as soon as the browser encounters it?  
True, unless the async or defer keywords are added to the ` script ` tag.
3. The defer keyword makes the browser wait until the document is loaded before running the JavaScript?  
TRUE.
4. Which of the options is correct?  
JavaScript is case-sensitive.
