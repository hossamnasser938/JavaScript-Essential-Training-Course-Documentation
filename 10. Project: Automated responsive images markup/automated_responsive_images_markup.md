# Automated responsive images markup

* This project aims to use JavaScript to solve the problem of **responsive images**.
* I understand **Responsive** as it means that the product(whether mobile app or web app) adapts to different screen sizes. So the app should look differently on different screen sizes. This is because bigger screen sizes allow to set the content in a way that small screen sizes do not.
* Responsive images refer to the ability to load different sizes of the same images on devices with different screen sizes since it is a waste to download a big image when you actually need a small one.
* Browsers provide some useful tools for developers. One of which is **Responsive Design Mode** which we can use to see how the app looks like on different screen sizes. To use it: ` Tools > Web Developer > Responsive Design Mode `.

* We used `slice` method with arrays before. Now we see this method on strings. `slice` is used in two different ways:
  * It can accept one argument which is the start index. In this case it returns the substring starting from this index till the string end. For example:
  ```js
  var s = "Hossam";
  console.log(s.slice(3));  // Output: sam
  ```
  * It can accept two arguments: the start index and the end index(The character of the end index is not included in the output). For example:
  ```js
  var s = "Hossam Abdelnaser";
  console.log(s.slice(7, 10));  // Output: Abd
  ```
  Note: if any one of the arguments is negative, the index is calculated in this way `strLength + param` where param is the negative argument. For example:
  ```js
  var s = "Hossam Abdelnaser";
  console.log(s.slice(-3));  /* The index calculated = strlength - 3 = 17 - 3 = 14. Output: ser */
  console.log(s.slice(-9, -3));  /* The indices is calculated = (17-9, 17-3) = (8, 14). Output: bdelna */
  ```

* Custom data attributes is a new feature in HTML5 that lets you store data related to DOM elements and easily access this data in JavaScript. To make one: name it like this "data-something" and something is whatever. The point is its name should start with "data-". Add it directly to the DOM element you want and access it in JavaScript easily using the method ` getAttribute ` and pass the name you have chosen for your custom data attribute.

* To support responsive images we need to add two new attributes to ` <img> ` tags. These attributes are:
  1. ` srcset ` which is a string of comma-separated list of strings. Each string is compsed of:
      1. image src.
      2. _optionally_ white space followed by either a width descriptor which is the width of the image followed by 'w' character(ex: "400w") or a pixel density descriptor which is the density number followed by character 'x' (ex: "4x").  
  
  An example that shows how to generate this list is the following. Suppose that the image src are in this format: "images/testimonials/zerog-400.jpg" and we need to add those srces: "images/testimonials/zerog-800.jpg", "images/testimonials/zerog-1200.jpg" ,"images/testimonials/zerog-1600.jpg" ,"images/testimonials/zerog-2000.jpg"
  ```js
  const IMAGES = document.querySelectorAll("img");
  
  function generateSrcSet( imgScrc ) {
    let srcSet = [];
    let width = 400;
    for ( let i = 0; i < 5; i++ ) {
      let currentWidth = width + width * i;
      srcSet[i] = imgSrc + currentWidth + ".jpg " + currentWidth + "w";
    }
    return srcSet.join();
  }
  
  IMAGES.forEach( function( element ) {
    let imgSrc = element.getAttribute("src");
    imgSrc = imgSrc.slice(0, -7);
    let srcSet = generateSrSet(imgSrc);
    element.setAttribute("srcset", srcSet);
    let imgType = element.getAttribute("data-type");
    console.log(imgType);
  });
  ```

  **A few comments**:
    * We used the ` slice ` method to cut this part "-400.jpg" which is 7 characters.
    * We accessed our custom data attribute which we named ` data-type ` using ` element.getAttribute("data-type") `.
    * We defined a variable to be an array by assigning to it an empty brackets ` let srcSet = []; `.
    * We used the ` join ` method with arrays to combine array elements in a single comma-separated string of those elements. We did this to prepare tha value of the ` srcset ` attribute.
  
  2. ` sizes ` which is a set of comma separated list of strings . Each string is composed of media condition and their appropriate images width.
  ```js
  sizes = "<media condition> <width>,
      <media condition> <width>,
      <optional default width>"  
  ```
    1. ` media condition ` is a condition that identifies different screen sizes. For example the media condition ` ( min-width: 900px ) ` identifies screen sizes with width more than 900px.
    2. ` width ` specifies what width should the image takes on this media condition.  For example the width ` 100vw ` specifies that the image should take the **full width(100%)** of the **view port(visible area of a web page)**.  
    An example that shows how to specify the sizes property using JavaScript is the following. Suppose that we have 4 different types of images(showcase, feature, reason, story). Those types are identified using the custom data attribute ` data-type `. So we define different sizes for different types of images.
        1. First we define an object to hold those different images sizes:
        ```js
        var SIZES = {
          showcase: "100vw",
          feature: "(max-width: 799) 100vw, 372px",
          reason: "(max-width: 799) 100vw, 558px",
          story: "(max-width: 799) 100vw, 670px"
        };
        ```
        2. Then we set the ` sizes ` attribute to one of those sizes to the ` <img> ` based on its data type.
        ```js
        IMAGES.forEach( function( element ) {
          let imgSrc = element.getAttribute("src");
          imgSrc = imgSrc.slice(0, -7);
          let srcSet = generateSrSet(imgSrc);
          element.setAttribute("srcset", srcSet);
          let imgType = element.getAttribute("data-type");
          console.log(imgType);
          let sizes = SIZES[imgType];
          element.setAttribute("sizes", sizes);
        });
        ```
