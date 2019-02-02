## Variables: The catch-all containers of JavaScript
* In programming we need some sort of **storage containers** that hold the data to be processed.
* A variable is a type of storage container that stores whatever data we put into.
* Since JS is a **weekly-typed language**, you do not have to specify the type of the data to be put in the variable when declaring it.
```
var var_name;
```
That's how we declare a variable in JavaScript.
* var_name can be any sequence of uppercase letters, lowercase letters, digits, dollarsign($), or underscore(_). However, we should not start the name of the variable with a digit.
* Once you declared the variable, it is empty or undefined. Now you can assign it a value, an object or another variable using the equal(=) operator.
```
var_name = 3;
```
* In JS we can use a variable without previously defining it. For example:
```
x = 5;
console.log("x = " + x);
```
Here I did not declare x but assigned it a value of 5. In this case JS will say "Ok, I will define it for you". However, this will introduce a problem because this variable will be defined with scope **global**.

## Data types in JavaScript
* We have six **primitive** data types in JS:
    * numeric.
    * string.
    * boolean.
    * null.
    * undefined.
    * symbol.
* A string value can be surrounded with single quotes(') or double quotes(").
* Null variable is a variable **intentionally** has **absent** value.
* Undefined variable is the variable that you get when you just declare the variable without assigning it a value. For example:
```
var x;
```
* To check the data type of a variable use the typeof **operator**. For example:
```
console.log(typeof x);
```
Recall that ` typeof ` is an **operator** not a **function**.

## Arithmetic operators and math
* In JS we have a bunch of operators:
    * Assignment operator: =
    * Arithmetic operators: +, -, *, /
    * Shorthand assignment operaors: +=, -=, *=, /=
    * Unary operators: ++, --

## Working with strings and numbers
* In addition to **"+"** operator being arithmetic operator, it is also a string operator. It means **concatenation**. For example:
```
var count = 5;
var s = "count = " + count;
```
Here the value of s is the string "count = 5".
* Consider this example:
```
var a = 4;
var b = "5";
var c = a + b;
console.log(c);
```
This script will output "45". This is not strange. Since one of the variables is a string the **"+"** operator is treated as a string operator not an arithmetic one.
* Consider this example:
```
var a = 4;
var b = "5";
var c = a * b;
console.log(c);
```
This script will output 20. Although b is a string and can not be multiplicated, JS will say "Since **"*"** is an arithmetic operator, so ofcourse you wanna use b as a numeric type and I will convert it for you".
* **NaN** means **not a number**. You get it when you try to do some maths with non-numeric things and even JS can not convert these things into numbers.

## Conditional statements and logic
* Conditional statements exist to help you control where to go based on some condition.
* ` If ` statement is the most popular:
```
if( some condition ) {
    Do_something
}
```
* ` If-else ` also exists:
```
if( some condition ) {
    do_something
}
else {
    do_something_else
}
```
* To check the **equality** of two variables or values, use the equality operator(==):
```
if(a == b){
    console.log("a is indeed equal to b");
}
else {
    console.log("a is not equal to b");
}
```
* Consider this example:
```
var a = 5;
var b = "5";
if(a == b){
    console.log("a is equal to b");
}
```
This script will output "a is equal to b". Again JS notices that 5 is equal to "5" so it evaluates it to true. What if we need to check if two variables are **identical**?
In this case use the **strict equality** operator(===). For example:
```
var a = 5;
var b = "5";
console.log(a === b);
```
This script will output **false** because yes 5 equals "5" but they are not **identical**. 5 is a number and "5" is a string.
* !== means **not** strictly equal.
* ! is pronounced **bang**.
* The **strict equality** operator as well as the **equality** operator can be used to check the equality of two strings.

## Advanced conditions and logic
* For logical **AND** operation we use two **ampersands(&&)** and for logical **OR** operation we use two **vertical lines or pipes(||)**.
* There is no logical **XOR** operation in JS. We have to do it manually.
* There is a simpler form for ` if-else ` statement. It is the **ternary operator**.
```
(some condition)? do_something : do_something_else;
```
* For example:
```
var a = 4;
var b = 5;
(a == b)? console.log("a is equal to b"): console.log("a is not equal to b");
``` 
Thus script will output "a is not equal to b".

## Arrays
* An array is the best choice for storing several related items like a list of things for example a list of students grades.
```
var grades;
grades = [95, 80, 90, 99, 50, 60];
```
* That was the shorthand form. We could do it in another way:
```
var grades;
grades = new Array(95, 80, 90, 99, 50, 60);
```
* Recall that an array is not a variable. It is an object.
* An array can hold items of the same data type and also can hold data of different data types.
```
var things;
things = ["string", 10, false];
```
* Yu can access array items simply.
```
var grades = [10, 7, 90];
var item = grades[0];
console.log(item);
grades[0] = 20;
console.log(grades[0]);
```
This script will output:  
10  
20  

## Properties and methods in arrays
* An array is an object.
* Objects hava properties and methods.
* Properties are peices of information describing the identity of the object.
* Methods are functions that define the behaviour of the object.

* To access a property of an object, simply ` objectName.propertyName ` . For example:
```
var colors = ["red", "green", "blue"];
log.console("colors length = " + colors.length);
```
we will use this array ` colors ` for future code.

* Arrays have many methods. We will see some of them.
    * ` reverse ` used to reverse the items within an array. ` reverse ` reverses **in place**. It **returns** a reference to the **original** array which is now reversed.
```
colors.reverse();
console.log("colors: " + colors);
```
output: ["blue", "green", "red"]
    * ` shift ` removes rhe first element of the array(the element at the left). ` shift ` **returns** the shifted item.
```
colors.shift();
console.log("colors: " + colors);
```
output: ["green", "blue"]
    * ` unshift ` adds items at the start of the array. ` unshift ` **takes** as arguments the items to be added and **returns** the new length of the array after adding items.
```
colors.unshift("purple", "yellow");
console.log("colors: " + colors);
```
output: ["purple", "yellow", "red", "green", "blue"]
    * ` pop ` removes the last item from the array and **returns** that item.
```
colors.pop();
console.log("colors: " + colors);
```
output: ["red", "green"]
    * ` push ` adds items to the end of the array. ` push ` **takes** arguments the items to be pushed and **returns** the new length of the array after adding items.
```
colors.push("purple", "yellow");
console.log("colors: " + colors);
```
output: ["red", "green", "blue", "purple", yellow"]
    * ` splice ` changes the content of the array by removing, replacing, or adding items. ` splice ` input arguments varies depending on the purpose, and **returns** an array containing the removed items.
        * removes a number of items from the array. For that purpose ` splice ` **takes** two arguments: The first is the index to start removing from and the second is the number of items to be removed.
```
colors.splice(1, 2);
console.log("colors: " + colors);
```
output: ["red"]
        * replaces a number of items with a number of items. For that purpose ` splice ` **takes** an unlimited number of arguments: The first is the index to start removing items from and adding the new items, the second is the number of items to be removed, and the rest of arguments are the items to be added.
```
colors.splice(1, 1, "purple", "yellow");
console.log("colors: " + colors);
```
output: ["red", "purple", "yellow", "blue"]
        * adds a number of items starting from a specific index. For that purpose ` splice ` takes an unlimited number of arguments: the first is the index to start adding items from, the second is the number of items to be removed and for **adding** purpose this argument should be zero, and the rest of arguments are the items to be added.
```
colors.splice(1, 0, "purple", "yellow");
console.log("colors: " + colors);
```
output: ["red", "purple", "yellow", "green", "blue"]
    * ` slice ` makes a copy of the array and **returns** the reference of that copy. Recall that any change on the copy does not affect the original array. They are now two different objects.
```
var copy = colors.slice();
console.log("original: " + colors);
console.log("copy before: " + copy);
copy.push("purple");
console.log("copy after: " + copy);
```
output:  
original before: ["red", "green", "blue"]  
copy before: ["red", "green", "blue"]  
copy after: ["red", "green", "blue", "purple"]  
original after: ["red", "green", "blue"]
```
    * ` indexOf ` searches for a specific item within the array and returns its index if exists if not returns -1 indicating that the item does not exist within the array. ` index ` can be given as arguments the item to be searched for only or we can add an index to start searching from.
```
var indexofBlue = colors.indexOf("blue");
if(indexOfBlue == -1)
    console.log("blue does not exist");
else
    console.log("blue exists at index " + indexOfBlue);
```
output: blue exists at index 2
    * ` join ` joins all array items together into a string. ` join ` can be called with no arguments and in this case the items within the string will be separated using comma(,). We can change this separator by giving ` join ` our separator as an argument.
```
var joinedItems = colors.join();
console.log("Items joined using comma: " + joinedItems);
joinedItems = colors.join(" | ");
console.log("Items joined using pipe: " + joinedItems);
```
output:  
Items joined using comma: red, green, blue  
Items joined using pipe: red | green | blue

## Chapter quiz
1. Which of these code examples is the correct way to declare variables?  
var a; a = 5;
var a = 5, b = 4, sum = a + b;
var a = 5;
2. A variable containing a string with only a number in it is treated like?  
A string or a number depending on the context it's used in.
3. The equals symbol = denotes equality?  
FALSE
4. What would be the value of sum in this code example: ` var a = 12, b = "3", sum = a + b; `?  
123
5. Given var a = 12 and var b = "12", will the conditional statement if (a === b) return true or false?  
FALSE
6. a || b (a OR b) is true when?  
a or b or both is true
7. The first item of an array has the index position 1?  
FALSE
8. How do you use a method on an object?  
Call the object followed by a punctuation mark, then call the method ending with parenthesis: myarray.reverse()
