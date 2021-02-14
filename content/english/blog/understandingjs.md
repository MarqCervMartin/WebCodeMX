---
title: "Understanding JS under the hood: var, let and const \U0001F9BE"
date: 2020-05-12T12:14:34.000+06:00
image: images/blog/understandingjs/understandingjs-1.jpg
tags:
- javascript
- development
description: Javascript.

---
<div class=text-justify>

Javascript is one of the top programming languages in this 2021 and I really love it, that’s why today we’re gonna talk about a topic that sometimes is very complex for beginners. To create truly powerfull and great apps, we need to understant how JS manage the variables, functions, call’s, etc. So, let’s talk about variables declaratations and how we have to be carefull in some cases.

#### ¿Javascript or ECMAScript?, ¿are they the same?

As we know JS is a programming language whose in the beginning just had the chance to be used in the web browser. **ECMAScript is the specification it’s based on. By reading the ECMAScript specification, you learn how to create a scripting language. By reading the JavaScript documentation, you learn how to use a scripting language.**

Browsers offers limitations between the standart (**JS engines, they interprete the code** ), every browser has a different JS engine, it’s like the specific kind of languaje that many parts of a country develop throughout time: english is not the same in Texas or New York. Or the latin spanish in “tepito” or Monterrey.

So, an engine can interprete a specific version of ECMAScript. When dev’s are asking for the ECMAScript version that a browser supports, they really are asking about the engine. Here’s a list that could help to understant better this concept:

![Engines and ECMAScript versions with browsers](https://web-code-mx.vercel.app/images/blog/understandingjs/undesrtandingjs-2.png "Engines and ECMAScript versions with browsers")

<center>Engines and ECMAScript versions with browsers</center>

Concluding this part, it’s important to know some limitations that a browser can have when yo’re writting code, well … you can use many tools (babel)to transform your code and forgot about this but that is another topic. <br></br>

#### Important concepts

1. **Scope**: It’s where these variables are available for use. This could be the entire context like all the windows or file about your writting code or the context inside a function.
2. **Hoisting**: Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution. That’s why you can call a function before to be declared. No matters where you write that declaration, js move it to the top of file or context, also we have to remember that js just move the declaration not the assignments.

#### ES5

**var**

Some years ago before ES6, using var was the most common and ruled way declaration. With var we have two scopes:

* Global scope: **Available in the entire window or file.**
* Function scope: **Available locally inside the function block.**

#### index.js

``` javascript
    var name1 = "I'm Jimmy";      //Global scoped

    function myFUnction(){
        var name2 = "I'm Carlos"; //Function scoped    

        console.log(name1)        //Output: I'm Jimmy
    }

    myFunction()
    console.log(name2) //Output: ReferenceError: name2 is not defined
```

<center>Using var</center>
<br></br>

As you can see in the image above, **“name1”** can be used inside the function but when we try to show **“name2”**, we’ll se a reference error because **“name2”** lives only in myFunction.

**Characteristics of var**

var variables can be **redeclared and reassigned,** for example:

#### index.js

``` javascript
    //First declaration and assignment
    var name = "Xavier"
    //Redeclarated
    var name = "Mr X"
    //Reassigned
    name = "Javier"

    //All this lines won't show any error
```

<center>This code won´t show error</center>

**Problem with var**

Imagine your code has a lot of lines and you declared an initial state or variable. Then you declared a variable with the same name inside a function, js won’t warn yout about this action and the system or app can crash or do a different behavior.

**Hoisting var**

We have to be awared that js engine moves the declaration of var variables to top but also initialize these variables to undefined.

#### index.js

``` javascript
    //What we write
    console.log(name) //output: undefined
    var name = "Alex"

    //What js understands (Hoisting)
    var name = undefined
    console.log(name) //output: undefined
    name = "Alex"
```

<center>Hoisting var</center>

**Special case:** If we don’t declared a variable but we assign a value to it, it does not exist until code assigning it is executed. Therefore, this behavior creates a global variable when the assignment is executed. **We most know that undeclared variables are global variables.**

#### index.js

``` javascript
    name = "Jimmy" //JS convert name into a global variable

    console.log(name) //output: "Jimmy"
```

<center>Undeclared variables are global variables</center>
<br></br>

#### ES6

**let**

Some of the problems of var came to be solved with ES6, today **let is the ruled of preferred variable declaration.** It solves the main problem with var.

* Block scope: A block is considered as a piece of code bounded by curly braces {}.

#### index.js

``` javascript
    let counter = 5

    if(counter > 1){
        let name2 = "I'm Carlos"; //name2 is block scoped
    }
    console.log(name2) //name2 doesn't exist here
```

<center>Block scope</center>
<br></br>

So, in the example above we see that **“name2"** no exists after the curly braces that bounded the if statement. To be sure, let’s se other example:

#### index.js

``` javascript
    let car = "Jetta Classic";
    let counter = 1
    if(counter > 0){
        let car = "Ferrari 2020";
        console.log(car); // "output: "Ferrari 2020"
    }
    console.log(car); //output: "Jetta Classic"
```

<center>This code won’t show errors</center>
<br></br>

With var, this piece of code could be read as redeclare “car” but that would be a mistake. Every variable in this example lives in it’s own scope, that’s why we see in the last line the value of the first assignment, we’re not changin the value of car, just declarating car in two scopes.

**Characteristics of let**

Unlike var, let could be reassigned but we cannot redeclare it in the same scope. If we do this, gonna get an error:

#### index.js

``` javascript
    let car = "Jetta Classic";
    let car = "Ferrari" //output: Identifier 'car' has already been declared
```

<center>Solves the problem with var</center>
<br></br>

**Hoisting let**

As we remember, js moves the var declaration assigning undefined on the top. In this case, the hoisting is almost the same but not assigning any value to the variable and showing reference error.

#### index.js

``` javascript
    //What we write
    console.log(name) //output: Cannot acces 'name' before initialization
    let name = "Alex"

    //What js understands (Hoisting)
    let name //Not assigned
    console.log(name) //output: Cannot acces 'name' before initialization
    name = "Alex"
```

<center>Hoisting let</center>
<br></br>

**const**

Using const variables is recomended if you want to maintain the value assigned to a variable in all the context. We have here the same similarities like using let. Also const is block scoped.

**Characteristics of const**

After the assigment with const, we cannot update the value. So, we cannot reassign or redeclare a variable.

#### index.js

``` javascript
    const pi = 3.1416

    pi = 3.15 //output: Assignment to constant variable
```

<center>With const, it’s not possible to redeclared or reassign a value</center>
<br></br>

**Hoisting const:** Just like let these declarations are hoisted but not assigned. **Also we cannot just declare a const variable, we most initialized it.**

<br></br>
After all this explanation, I hope your js knowledge will be better and more strong. Some times we talk about JS without understanding it under the hood, but when you cross the line you become a ninja ❤.

<br></br>

<img src="/images/blog/understandingjs/jimmy.jpeg" style="border-radius: 50%;float: right; " />

WRITTEN BY Jimmy Vasquez   <a href="https://jimmyvazz.medium.com/" target="_blank">Follow</a> | --- | :---: | ---: | Software Engineer📱 Editor on Nerd For Tech 👔  Geek ❤ Feb 1  5 min read  Javascript |

</div>