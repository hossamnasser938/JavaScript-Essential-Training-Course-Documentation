## Functions in JavaScript
* Functions are miniprograms that can be reused in our scripts.
* **Functions** allow us to **structure** our code and make common operations **reusable**.
    * **Structuring** our code means dividing it into segments so that it can be easily managed, tested and maintained.
    * **Reusability** helps avoiding redundancy by separating common operations into functions so that when one of these common operations is needed it is just called by a single line of code instead of writing it all again.
* Functions do one of two things:
    * Create an **effect** immediately like changing the content of a web page.
    * provide an **output**(called **return value**) to be used by other functions.
* In JavaScript we have three types of functions:
    1. Named functions  
Functions defined with a name. This name can be used to call or invoke the function later.  
Definition:
```
function sum(a, b){
  return a + b;
}
```
Invokation:
```
var c = sum(3, 4);
```
    2. Anonymous functions  
Functions with no names. They can be stored in a variable and called using the name of that variable or can be given as a parameter to another function.
```
var anonymousFun = function(){
  console.log("I am an Anonymous function");
}
anonymousFun();
```
    3. Immediately invoked function expressions  
Executed by the browser as soon as it encounters them.
```
(function(){
  console.log("I am an immediately invoked function expression");
}())
```
* These types of functions will be illustrated later.
* It is best practice to define the function before calling it. This helps humans reading your code.
* Each function has an arguement's object which is an array of possible arguments that can be passed to the function when calling it.

## Add arguments to the function
* Defining a funcion that accesses variables from outside the function limits the reusability of the function because the execution of it now depends on those variables.
```
function whichIsBigger(){
  a > b ? console.log(a + " is bigger"): console.log(b + " is bigger");
}
var a = 3 / 7, b = 5 / 8;
whichIsBigger(a, b);
```
The function whichIsBigger depends on the variables a, b. This limits its reusability and portability.
* Instead define those variables as arguments for the function.
```
function whichIsBigger(a, b){
  a > b ? console.log(a + " is bigger"): console.log(b + " is bigger");
}
var n1 = 3 / 7, n2 = 5 / 8;
whichIsBigger(n1, n2);
```
Now the function whichIsBigger can operate on any variables or values given as input arguments.

## Return values from a function
* Previously we defined the function whichIsBigger which compares two fractions and **logs** the biggest of them. Sometimes we want to decide what to do with the biggest later, whether to log it, store it, pass it to another function or whatever. In this case we can just define whichIsBigger to **return** the biggest and let what can be done is decided later.
```
function whichIsBigger(a, b){
  var biggest;
  a > b ? biggest = a: biggest = b;
  return biggest;
}
var n1 = 3 / 7, n2 = 5 / 8;
var result = whichIsBigger(n1, n2);
```

## Anonymous functions
* An anonymous function is a function with no name. So how can we call it when it does not have a name? 
* For an anonymous function be called manually it must be assigned to a variable. When it is assigned to a variable we can call the function using the variable name exactly as if it were a function name.
    * Definition: 
```
var biggest = function(a, b){
  a > b ? console.log(a + " is bigger"): console.log(b + " is bigger");
}
```
    * Invokation:
```
biggest(3 / 4, 5 / 7);
```
* Ofcourse you ask why we need anonymous functions? 
    * When defining events you may want to define a function to be called when that event occurs. Since the function will be called by the event not you, the function does not have to have a name. It is just sufficient to be **tied** with its event somehow.

## Immediately invoked function expression
* What happens if we logged variable that contains an anonymous function.
```
console.log(biggest);
```
Actually you will see the **code** in this anonymous function because that is what the variable holds.

* Immedialtely invoked function expressions(IIFE) are functions that are executed by the browser immediately as soon as the browser encounters it. In other words you define it and immediately call it.
* IIFE syntax:  
```
(function(a, b){
  a > b ? console.log(a + " is bigger"): console.log(b + " is bigger");
})(5 / 7, 8 / 9);
```
or if we want the IIFE to return a value:
```
var biggest = (function(a, b){
  a > b ? return a: return b;
})(5 / 7, 8 / 9);
```
* Now what if we logged the variable biggest.
```
console.log(biggest);
```
Would we get the code of the function? No, we would get the output of the function which is in this case the biggest from (5 / 7, 8 / 9).
* You may now wonder why we wrap a block of code in a function if we will call it just once. Why not we simply execute this with no function? Untill now I have no idea.

## Variable scope
* The scope of a variable is where in your code the variable is accessible.
* The location of the variable declaration decides the scope of the variable.
* We have two different scopes:
    * Global scope  
A global variable is a variable that is declared outside any function in the root of the script so that it can be accessed from all functions or anywhere in the script.
    * Local scope  
A local variable is a variable that is declared within a **block**(function for example) so that it can be accessed **only** in that block.
* You should be aware about declaring global variables. There are so many reasons that make you aware of this. One of them is that they exist in the browser memory as long as the script is running. Unlike local variables they exist for the execution of their block and then discarded by the browser.

## let and const
* ES6 introduced two new types of variables ` const ` and ` let `.
    * ` const ` declares a **constant** variable that once it is assigned a value it can be reassigned or updated. This is very useful in some cases like defining maths constants for example the **pi** constant.
```
const PI = 3.14;
console.log("PI = " + PI);
```
now if you tried to update the PI constant **intentionally or not** you will get an error.
    * ` let ` is a block-scope variable. A scope that is **smaller** than local.
```
function checkAge(age){
  if(age > 15){
    let state = "old enough"
    console.log(state);
  }
}
```
here the ` state ` variable has scope of only the if block not the whole function. Thus if we tried to access this variable outside the if inside the function like this
```
function checkAge(age){
if(age > 15){
let state = "old enough"
}
console.log(state);
}
checkAge(20);
```
We will get an error ` ReferenceError: state is not defined `.  
Unlike other programming languages, JavaScript treats variables defined with ` var ` keyword inside an inner block of a function as if it were declared outside the inner block inside the function itself. So if we declared ` state ` using ` var ` inside ` if ` statement we still can access this variable anywhere inside the function. Thus this code is executed with no problem.
```
function checkAge(age){
  if(age > 15){
  var state = "old enough"
  }
  console.log(state);
}
checkAge(20);
```
Output: old enough
 
## Make sense of objects
* JavaScript is an object-oriented language with flexibility towards object orientation. Guess what? JavaScript has no classes.
* How is JavaScript a **scripting language** and also **object-oriented** language?
* Actually there is no formal specification for object-oriented paradigm. There is no standards that allow categorizing a programming language as object-oriented or not. But from a fast reading: two requirements must be met to accept a language as object-oriented one:
    * capability of modeling a problem using objects.
    * support of a few principles that permit modularity and code reuse(encapsulation, inheritance, polymorphism).  
Ref: [Medium article](https://medium.com/@andrea.chiarelli/is-javascript-a-true-oop-language-c87c5b48bdf0)
* Objects are needed to model a cluster of data related to a specific entity and defining what actions can be done on that data.
* Technically, objects are data models that allow us to combine properities and methods for a specific data set in a structured way.
* In JavaScript we simply create an object without previously defining a class:
```
var course = new Object();
```
* After creating the object we can specify its attributes and their values.
```
course.title = "JavaScript Essential Training";
course.instructor = "Morten Rand-Hendriksen";
course.views = 0;
```
* We can also add functions to that object.
```
course.addViews = function(v) {
  course.views += v;
  return course.views;
}
```
* We could do all of that using the shorthand way.
```
var course = {
  course.title : "JavaScript Essential Training",
  course.instructor : "Morten Rand-Hendriksen",
  course.views : 0,
  addViews : function(v) {
    course.views += v;
    return course.views;
  }
}
```
* Now we can log the whole object or access a specific property within it.
```
console.log(course);
console.log("course views number = " + course.views)
```

## Object Constructors
* It is intuitively **inefficient** to define the attributes and functions for each object we create. We want to define those once.
* This can be done easily using **object constructors**.
```
function Course(title, instructor, views){
  this.title = title;
  this.instructor = instructor;
  this.views = views;
  this.addViews(v){
    this.views += v;
    return this.views;
  }
}
```
Now we can use that consructor to instantiate many Course objects. Recall that ` this ` here refers to the ` var ` that will be populated using the constructor(c ` var ` in the next example).
```
var c = new Course("JavaScript Essential Training", "Morten Rand-Hendriksen", 0);
```

## Sidebar: Dot and Bracket notation
* In JavaScript we have two different notations to access properties of objects:
    * Dot notation  
which we are familiar with.
```
console.log(c.title);
```
    * Bracket notation  
which we use in two situations:
        * to access properties with names that may contain operators like (emp:name). If we tried to use **Dot motation** JS will consider **:** as an operator and it will get confused.
```
console.log(c["emp:name"]);
```
        * to get properties that we have their names stored in variables.
```
const TITLE_PROPERTY = "title";
console.log(c[TITLE_PROPERTY]);
```

## Closures
* Consider the following script:
```
function sayHello(name){
  return function(){
    alert("Hello " + name + "1");
  };
}
var helloHos = sayHello("Hosam");
var helloSo = sayHello("Soad");
```
Here we created a function that returns an anonymous inner function so the variables ` helloHos ` and ` helloSo ` contains the code block of the inner function, right?  
If that is the case what will happen when executing the inner function by calling ` helloHos(); ` or ` helloSo(); `? Intuitively it will generate an error because it know nothing about the variable ` name ` used in the ` alert ` statement. However, it will work perfectly. That is because of **closures**.  
* A **closure** is a function wrapped with its **lexical environment**. This means that the variables ` helloHos ` and ` helloSo ` not only contain the inner function but also its lexical environment or the variables and functions defined in its scope. In this case the lexical environment is only the variable ` name `. That's why the previous script runs with no errors.
For practical use of closures refer to this article [MDN Article on closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures).

## Chapter quiz
1. Functions execute as soon as they are read by the browser?  
FALSE
2. Variables defined before a function call are available to the function?  
TRUE
3. An argument passed to a function must have the same name in the function call and the function itself?  
FALSE
4. What happens when you use the return statement in a function?  
The returned value is sent back to wherever the function was called. 
5. Anonymous functions receive arguments?  
TRUE 
6. Immediately Invoked Function Expressions _____?  
execute as soon as the browser reads them 
7. Which statement is accurate?  
A variable declared inside a function is only available inside that function. 
8. In JavaScript, any element listed before a period is treated as an object?  
TRUE  
A period is a dot(.).
9. What happens if you create a new object using an object constructor, but don't add all the necessary arguments to declare all properties?  
The object is created with the undeclared properties set to "undefined."
10. Define "closure."?  
A function that remembers the environment they were created in.
