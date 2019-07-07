## DOM: The document object model
* The browser is an object and it has many objects inside including the browser window, the document inside the window, the navigation buttons, URL and more.
* These objects are modeled using the Browser Object Model(BOM).
* The window object is the top-level object in the BOM.
* The object inside the window object that we will interact with all the time is the ` document ` object which holds the current html content.
* We can get the document object by ` window.document ` or simply ` document ` since JavaScript lives inside the window.
* The ` document ` object is modeled using the Document Object Model(DOM).
* For me, the reason why we need to model these objects using BOM and DOM is to make the interaction with them the same independently from the type of the browser.

## Target elements in the DOM with querySelector methods
* To access elements inside the DOM we have two different situations:
  * High-level elements such as **title, body, url** and more can be accessed using the **dot** notation that we are familiar with.
  ```js
  document.body
  document.title
  document.URL
  ```
  * To get to a node or a group of nodes inside the body we can use methods such as:
  ```js
  document.getElementById("some_id")
  document.getElementsByClassName("some_class_name")     // returns a NodeList object
  document.getElementsByTagName("some_html_tag")	      // returns a NodeList object
  ```
  We also have two methods that are more specific:
    * the method ` querySelector("some_css_selectors") ` which gets the first item in the DOM that mathces a specified css selector(note that a css selector can be an ID, a className or tagName but it should be followed by dot in case of a className, hash in case of an ID, and nothing in case of tagName).
    * the method ` querySelectorAll("some_css_selectors") ` does the same as ` querySelector ` but instead of returning the first element matching the given css selectors, it returns all elements matching these selectors in the DOM.  
    Note: you can give more than one css selectors as input parameters to the ` querySelector ` and ` querySelectorAll ` methods.

## Access and change elements
* After getting the element we need using either one of the methods presented before we can read or update this element.
```js
document.querySelector(".student_name").innerHTML = "Hossam";
document.querySelector(".student_name").outerHTML = "<h1>Hossam</h1>"
```
The difference between the properties ` innerHTML ` and ` outerHTML ` is that the first references the value inside the element while the second references the whole element.

## Access and change classes
* Not all element's properties are overritable. Some of them are read-only.
* For those properties that are read-only there are methods defined to enfoce a certain way of writing to them.
* For the property ` classList ` which contains an array of class values associated with the element, we have those methods:
    * ` add() ` used for adding class values to the list. It **takes** as arguments any number of class values.
    ```js
    document.querySelector(".gLFyf").classList.add("new-class");
    ```
    Notice ` new-class ` without dot.
    * ` remove ` used to remove any number of values.
    * ` item() ` used to retreive a value with its index. This can be done using bracket notation since classList is an array.
    ```js
    document.querySelector(".gLFyf").classList.item(0);
    ```
    the same as:
    ```js
    document.querySelector(".gLFyf").classList[0];
    ```
    * ` contains() ` used to check whether the elements has a specific value or not.
    ```js
    document.querySelector(".gLFyf").classList.contains("gsfi");
    ```
    Notice also ` gsfi ` without dot.
    * ` toggle() ` used to enable/disable a specific value. This method can have one input or two inputs. 
        * In case of two inputs: the first is the value to enable/disable and the second is a boolean: true -> enable, false -> disable. 
        * In case of one input: it is a string representing a value then:
            * if the value exists then remove it(disable).
            * if it does not exist then add it(enable).

## Access and change attributes
* The ` attributes ` property is also read-only so we have these methods to deal with it:
    * ` hasAttribute() ` checks whether the element has a apecific attribute or not.
    ```js
    document.querySelector(".gLFyf").hasAttribute("href");
    ```
    * ` getAttribute() ` returns the value of a specified attribute. If the attribute does not exist the return value will either be ` null ` or ` "" ` the empty string.
    * ` setAttribute() ` adds a specific attribute and its value. It takes as arguments the name of the attribute and its value.
    * ` removeAttribute() ` removes a specific attribute.

## add DOM elements
* To add a node in the DOM, we can do that by getting the element we want our new element to be under and using the properties ` innerHTML ` and ` outerHTML ` we can do tha job. However, this will make us write a lot of HTML code in our script and any mistake will lead to an error loading the document.
* We have a better way to do that:
    1. create a new element using the method ` createElement() ` and pass the element tag as an argument.
    2. create a text node(the content inside that element) using the method ` createTextNode() ` and pass the text as an argument.
    3. append this text node to the new element using the method ` appendChild() ` and pass the text node as an argument.  
Until now you have just created the new element.
    4. Find the element that you want to insert the new element under using the method ` querySelector() `.
    5. add the new element to that element using the method ` appendChild() `.  
    Here is an example:
    ```js
    const NEW_ELEMENT = document.createElement("figcaption"); // step 1
    const NEW_TEXT_NODE = document.createTextNode("Menofia university"); // step 2
    NEW_ELEMENT.appendChild(NEW_TEXT_NODE); // step 3
    const FIG_ELEMENT = document.querySelector(".featured-image"); // step 4
    FIG_ELEMENT.appendChild(NEW_ELEMENT); // step 5
    ```
* The procedure above is too long but it works with all browsers. We can simplify it a little bit but the upcoming is not supported by old browsers.  
We can wrap steps 2 and 3 into one. Instead of:
```js
const NEW_TEXT_NODE = document.createTextNode(CAPTION_TEXT); // step 2
NEW_ELEMENT.appendChild(NEW_TEXT_NODE); // step 3
```
we can use ` append ` method.
```js
NEW_ELEMENT.append(CAPTION_TEXT);
```
* If we have a reference to a DOM element and we want to find an element inside it instead of traversing the full tree.
```js
const OUTER_ELEMENT = document.querySelector(".featured-image");
const INNER_ELEMENT = OUTER_ELEMENT.querySelector("img");
```
Here we used the outer element to find the inner element instead of traversing the full tree again.

## Apply inline CSS to an element
* JavaScript also can play around with style(CSS). However, it has no access to styles in external files(CSS files) or even style declared in the ` head `. It just can play around with the ` style ` attribute of any element(inline CSS with individual elements). We have two different ways to do that:
  * add one style rule to the style attribute.  
  We do that by accessing the rule we wanna set in the style and assign it a value.
  ```js
  document.querySelector(".cta").style.color = "green";
  ```
  This will keep the style string as it and just concatenate it with the new rule related to color ` color: green; `.  
  Hint: if a style name like ` backgroud-color ` it can be accessed using camalcase ` style.backgroundColor `.
    * override the whole style string with a new one.  
    ```js
    document.querySelector(".cta").style.cssText  = "color: green; padding: 2em;";
    ```
    This will override what was inside the style attribute with the new string ` "color: green; padding: 2em;" `.
    Another way to do that:
    ```js
    document.querySelector(".cta").setAttribute("style", "color: green; padding: 2em;");
    ```
    Here we treat the style as a normal attribute and use the ` setAttribute ` method with it.

## Chapter quiz
1. What will document.querySelectorAll([query selectors]} return?  
an HTML NodeList containing all document nodes matching the specified query selector
2. Using the classlist methods on an element changes the _____?  
classes applied to that element in the current browser window .
3. You can target most, but not all, element attributes using JavaScript?  
FALSE
4. Where is a new element created using the createElement() method added?  
In the browser memory only. To add it to the document you must use the appendChild() or append() methods.
5. The style property of an element gives you a list of all styles applied to that element?  
FALSE: The style property only lists the inline styles.

