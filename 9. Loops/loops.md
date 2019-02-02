## Loops
* A loop is what enables us to execute a block of code for more than once.
* Loops in JavaScript are not different from most programming languages(Till now).
* We have three types of loops:
    1. `for` loop lets us execute a block of code a **given** number of times.
```
for (var i = 0; i < 10; i++) {
  console.log(i);
}
```
    2. `while` loop lets us execute a block of code as soon as some **condition** hold.
```
var i = 1;
while (i < 325) {
  console.log(i);
  i *= 2.3;
}
```
    3. `do while` loop does the same as `while` loop but the difference is that `do while` loop **executes and then check** which ensures that the code block wrapped in the `do` **will get executed for at least once**.
```
var i = 325;
do {
  console.log(i);
  i *= 2.3;
} while (i < 325);
```
The output of the `do while` loop in this example is: 325 . However, if we used the while loop like this:
```
var i = 325;
while (i < 325) {
  console.log(i);
  i *= 2.3;
}
```
The output is nothing since the condition does not hold for the first time.

## Looping through arrays
Let's see our first practical example using loops. We wanna get all external links in a document and make sure that each one has the `target` attribute set to "\_blank".
```
const EXTERNAL_LINKS = document.querySelectorAll('a[href^="http"]');
for ( var i = 0; i < EXTERNAL_LINKS.length; i++ ) {
  if ( !EXTERNAL_LINKS[i].hasAttribute("target") ) {
    EXTERNAL_LINKS[i].setAttribute("target", "_blank");
  }
}
```
#### Some comments:
* We used `querySelectorAll` function to get all the elements with given CSS selectors.
* `'a[href^="http"]'` this selector means all **links** (`a`) that has **attribute** (`href`) with value **starts** with **http**(`href^="http"`).

#### Alternative way
In most programming languages, we have `for each` syntax to facilitate looping through array elements. In JavaScript we have `forEach` defined as a **method** on Arrays. `forEach` accepts as arguments a function that accepts the element of the array to be executed on. We can use `forEach` to accomplish the same goal.
```
const EXTERNAL_LINKS = document.querySelectorAll('a[href^="http"]');
EXTERNAL_LINKS.forEach( function( element ) {
  if ( !element.hasAttribute("target") ) {
    element.setAttribute("target", "_blank");
  }
  } );
```
Note: this is another good use case of **Anonymous function**.

## Break and continue loops
* `break` keyword is used to terminate the current loop and go straight to the statement that follows the loop. To illustrate the idea let's generate random numbers between(0:30) until we generate the number 17.
```
const MIN = 0, MAX = 30;
const EXCEPTION = 17;
var i = 0;
while ( true ) {  // loop for ever
  i++;
  // get a random number in the range MIN:MAX
  let randomNumber = Math.floor(Math.random() * (MAX - MIN)) + MIN;
  if ( randomNumber == EXCEPTION ) {
    break;
  }
  console.log( randomNumber );
}
console.log("We looped " + i + " times before hitting the exception " + EXCEPTION);
```

* `continue` keyword is used to skip the current iteration of the loop and go straight to the next one. To illustrate the idea let's get the prime numbers between 50 and 100.
```
const FLOOR = 50;
const CEILING = 100;
function isPrime(n){
  if ( n < 2 ) {
    return false;
  }
  if ( n > 2 && n % 2 == 0 ) {
    return false;
  }
  for ( var i = 3, s = Math.sqrt(n); i < s; i += 2 ) {
    if ( n % i == 0 ) {
      return false;
    }
  }
  return true;
}
for ( var i = FLOOR; i <= CEILING; i++ ) {
  result = isPrime(i);
  if( result == false ) {
    continue;
  }
  console.log(i + " is prime : " + result);
}
```

## Chapter quiz
1. When you run a do/while loop, the do function runs first, then the while condition is checked, and if true the loop goes through another iteration?  
TRUE
2. What does the continue keyword do in a loop?  
Skip the remainder of the code block before continuing on to the next iteration of the loop.
