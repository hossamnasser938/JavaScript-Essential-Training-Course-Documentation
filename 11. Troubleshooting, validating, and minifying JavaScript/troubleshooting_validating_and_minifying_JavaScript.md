## JavaScript validation and troubleshooting
* JavaScript sometimes behave in a very strange way so it is a goof idea to address **validation** and **troubleshooting**.
* **Validation** is the process of checking or proving the validity(correctness and accuracy) of something or ,simply, proving that a product or service does what it is intended to do.
* **Troubleshooting** means getting involved to see what's wrong and solve problems.
* This chapter introduces us to a set of tools that we can use in validation and troubleshooting:
    * Validation tools.
    * Delinters: machines that remove lints(cotton used with wounds)[We will see how this meaning reflects its purpose soon].
    * Bug_testing(debugging) tools.
    * Tips on how to troubleshoot your code to catch problems earlier as soon as possible.

## Troubleshooting JavaScript
* Tip: Whenever you encounter the error ` Unexpected SyntaxError: Unexpected end of input ` or ` Unexpected SyntaxError: Unexpected end of input ` , definitely you forgot to close parenthesis, curly braces, or square brackets. For this type of error the code editor can help you by checking each parenthesis, curly brace, and square bracket is properly closed. If you get the cursor before or after the opening one or the closing one, the code editor highlights both.
* The second debugging tool is color coding. Methods, variables, numbers, strings, keywords, categories have different colors.

## Send troubleshooting info to the console
* ` console.log() ` is not the only function that you can use to output something on the console. Actually there are a bunch of methods there. The most useful two of them are:
    * ` console.info() ` displays an **i** icon discriminating info from other logs.
    * ` console.error() ` displaying **red** text indicating that it is an error.

* Remember the ` setInterval() ` method we used in lesson 8: **The typing speed test**. There is a big bug there let's catch it:
    * If the user types the first character we start an interval and store a reference to that interval in variable ` interval `.
    * If the user types the whole text correctly, we clear the interval.
    * If the user hits reset, we as well clear the interval.
    * The bug in this scenario: The user types some text(the interval started) that did not match the original text and then clear the whole text leaving the text area empty and starts typing again(a new interval started and we lost the reference to the first one). When the user finishes typing the whole text correctly the second interval will be cleared but the first one will not since we have overridden the variable ` interval ` and lost the reference to the first interval.
    * The solution is:
        1. Declare a boolean variable initialized with ` false `.
```
var timerRunning = false;
```
        2. When the user types the first character check before starting an interval that the variable is still ` false `, if so set the variable to ` true ` and start the interval.
```
function start() {
    let textEnterdLength = testArea.value.length;
    if (textEnterdLength === 0, !timerRunning) {
        interval = setInterval(runTimer, 10);
        timerRunning = true;
    }
}
```
        3. When the user hits reset, clear the variable to ` false ` and clear the interval.    
```
function reset(){
   clearInterval(interval);
   timerRunning = false;
   theTimer.innerHTML = "00:00:00";
   testArea.value = "";
   testWrapper.style.borderColor = "grey";
   errorsField.innerHTML = 0;
 }
```

## Step through your JavaScript with browser tools
* Browsers come with a very powerful tool for **debugging**. To access this tool open the **Sources** tab right to console. Using this tool you can:
    * Set break points to tell the browser stop here to see the state right now.
    * Execute your script line by line.
    * See how variables change in each step.
    * and many other useful features.

## Online script linting
* There are multiple tools that you can use to test the quality of your JavaScript code and make sure that you follow the **standards** and **best practices**.
* JavaScript is a very **flexible** programming language in the sense that it says now problem when you forget to add a semicolon at the end of any statement, forget to declare a variable before using it, and many other issues that JavaScript handles for you.   
* This **flexibility** however sometimes result in weirred things. So we use some tools to improve our scripts as well as coding habits.
* The most common tool for that purpose is **JSlint**. **JSlint** is a very powerful tool that helps you achieve high efficient code style. The problem with **JSlint** is that it concentrates on many issues that somebodies think that these are not necessary things such as indentation and suitable spaces between tokens.
* An alternative to **JSlint** is **JShint** which is yet a powerful tool with much flexibility than **JSlint** in the sense that it concentrates on the important issues with your script that affect the quality.

## Automate script linting
* Using an online tool for the purpose of **linting**(treating wounds or simply solving issues) requires you all the time to copy your script source code, go online, paste it, and see the report. This is a lot of headache. Alternatively we can add a linting tool to our text editor(__Atom__).

* For this purpose, We can use **ESlint** to do the job. Here are the steps to integrate it with __Atom__:
    1. Make sure **Node.js** and **NPM**(Node Package Manager) installed.
    2. Install **ESlint**(as a command-line tool) by hitting this command ` sudo npm install -g eslint `. Here ` -g ` means globally.
    3. Install **ESlint** on **Atom**(Go to packages -> settings view -> open -> install-> packages, search for eslint, and install it).

* To use **ESlint** you have to configure it with each individual project you work on by following these steps:
    1. Set an **NPM** environment for the project by hitting ` npm init `.
    2. Answer some questions or skip them.
    3. By now  you will have a file called ` package.json `(contains packages and dependencies) in your project directory.
    4. Initiate **ESlint** by hitting ` eslint --init `.
    5. Specify your optimal code style, use existing one, or let ESlint capture your optimal code style through a file.

## Online script minification
* Minification means removing all **unnecessary** things and optimizing the script to reduce its size and make it easier to be downloaded and run by the browser. Unnecessary things here mean things that the script can run **correctly** without such as white spaces, comments, etc.
* This will make the script completely unreadable for us humans. So we keep the two versions: the original readable one for further maintenance and the minified one which we reference in HTML so that it is the one to be downloaded by the browser.
* There are many minification tools online. One of them is **minifier**.
* As a convention, if your script named **script.js** you name the minified one **script.min.js**.
* If you tried to debug this minified script on the browser it is unreadable. Fortunately, the browser provides a button to unminify the script and make it again readable and easier to debug. This button is called **pretty print** denoted **{ }** appearing bellow the script on the **Sources** tab.

## Automate script minification
* As we did with linting, we wish to integrate a minification tool. In this case the tool works as just a command-line one independent of the text editor.
* There are many tools out there. One of them is **uglify-js**.
* To use it:
1. Make sure **Node.js** and **NPM**(Node Package Manager) installed.
2. Install it using ` sudo npm install -g uglify-js `.(if uglify-js still does not support ES6, use **uglify-js-es6** instead).
3. Head to where the script exists.
4. Open **Node.js command prompt** by hitting ` nodejs `.  
5. Hit ` uglify [original_script_name] -o [minified_script_name] ` where you replace ` original_script_name ` and ` minified_script_name ` with your scripts names.

## Chapter quiz
1. What is the first troubleshooting step when your JavaScript is not working as expected?  
Look for errors in the browser console.
2. You should use a JavaScript linter?  
TRUE
