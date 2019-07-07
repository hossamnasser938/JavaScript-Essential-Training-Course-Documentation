This project aims to build an analog clock running for ever.
* to repeatedly call a function with a fixed time delay between each call use the function ` setInterval() ` . The ` setInterval ` method accepts two arguments: the first is a reference to the function to repeatedly call and the second is the time delay between each call in milliseconds. ` setInterval ` method returns interval ID which uniquely identifies the interval so we can clear that interval in the future by calling ` clearInterval ` method and pass the interval ID as an argument.
```js
function sayHello(){
  console.log("Hello");
}
var interval = setInterval(sayHello, 1000);
```
This script will repeatedely call the function ` sayHello ` each 1 second. To clear the interval(stop calling this function).
```js
clearInterval(interval);
```
* Useful shortcuts:
    * to comment/uncomment a line(s) of code ` ctrl + / `.
    * to right indent a line(s) of code ` ctrl + ] `.
    * to left indent a line(s) f code ` ctrl + [ `.
    * to open the console on the browser ` ctrl + shift + i `
