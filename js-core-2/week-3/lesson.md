# JavaScript Core II - Week 3

---

**Teaching this lesson?**

Read the Mentors Notes [here](mentors.md)

---

## Contents

- [Synchronous and Asynchronous programming](#synchronous-and-asynchronous-programming)
  - [A real life example](#a-real-life-example)
  - [A Javascript example](#a-javascript-example)
  - [Callbacks](#callbacks)
    - [Exercise (1)](#exercise-1)
- [How does the web work?](#how-does-the-web-work)
  - [Client/Server architecture](#clientserver-architecture)
  - [HTTP Requests](#http-requests)
    - [Exercise (2)](#exercise-2)

---

## Learning Objectives

By the end of this lesson students should be able to:

- Define the difference between synchronous and asynchronous code
- Describe why writing asynchronous code is important when working with the internet
- Write code that is able to pass a function to another function as a parameter and run it
- Use callbacks to run code at some point in the future
- Define a client's and server's role in the client/server architecture
- Describe the difference between a GET and POST request
- Explain how resources are loaded on the internet using GET and POST
- List the steps that a browser does when loading a website from the internet

---

## Synchronous and Asynchronous programming

In a synchronous programming model, tasks run one at a time. When a long running action starts, the program waits for it to finish and return the result before it moves to the next action.

Asynchronous programming allows multiple actions to happen at the same time. When a long running action starts, the program can continue to run. When the action finishes the program will get notified and get access to the result returned.

![](assets/sync-vs-async.jpg)

### A real life example

An example of this in real life, are phone calls and text messages.

- Phone calls are `synchronous` because you can't (really) do anything while the
  other person is speaking. You are always waiting for your turn to respond
- Text messages are `asynchronous`. When you send a text, you can go away and do
  something else, until the other person responds.

### A Javascript example

```js
//synchronous
console.log("First action");
console.log("Second action");
console.log("Third action");
```

```js
//asynchronous
console.log("First action");
setTimeout(function () {
  console.log("Second action");
}, 1000);
console.log("Third action");
```

### Exercise (1)

```js
const greekGods = [
  "Aphrodite",
  "Ares",
  "Artemis",
  "Athena",
  "Poseidon",
  "Zeus",
];

// before running the code in your browser, discuss the expected order of each loop

// synchronous - loop through the array of greek gods and print the index numbers and values to the console, e.g. '1. Ares'

// asynchronous - same as before but the index and the value of the god at position 2 in array should be printed after 2 seconds. Use: setTimeout()
```

### Callbacks

We have already seen callback functions - in the Array methods `forEach`, `map`, `filter` etc. They are functions that are passed as parameter to another function.

In order to achieve asynchronicity, callbacks can be passed on functions that perform a slow action. By doing so, the callback function can be called with the result.
This allows you to run some other code while you're waiting for something to finish.

```js
function finished() {
  console.log("The task has finished");
}

function thingThatTakesALongTime(callbackFunction) {
  //... Task that takes a long time to complete

  callbackFunction(); // This is where the 'console.log' happens
}

// Pass the function to 'thingThatTakesALongTime' just like a normal variable
thingThatTakesALongTime(finished);
```

A simple example of an asynchronous function is `setTimeout`. This allows you to run a function after a given time period. The first argument is the function you want to run, the second argument is the `delay` (in milliseconds)

```js
// Separate function definition
function myCallbackFunction() {
  console.log("Hello world!");
}
setTimeout(myCallbackFunction, 1000);

// Inline function
setTimeout(function () {
  console.log("Hello world!");
}, 500);
```

Now let's use a timeout and a callback function together:

```js
function mainFunction(callback) {
  console.log("Starting!");
  setTimeout(function () {
    callback();
  }, 1000);
  console.log("Continuing!");
}
function myCallbackFunction() {
  console.log("Finished!");
}
mainFunction(myCallbackFunction);
```

#### Exercise (2)

> - Using setTimeout, change the background colour of the page after 5 seconds (5000 milliseconds).
> - Update your code to make the colour change _every_ 5 seconds to something different. Hint: try searching for `setInterval`.
>
> ![](http://g.recordit.co/g2EqBccNzh.gif)
>
> Complete the exercises in this [CodePen](https://codepen.io/makanti/pen/abOreLg?editors=1011)

#### Exercise (3)

> Complete the exercises in this [CodePen](https://codepen.io/textbook/pen/MWwMgmW?editors)
>
> - You are given a list of movie objects to work with<br/>
> - Use setTimeout to imitate that some actions take time
> - Remember that setTimeout behaves asynchronously
>
> All set, go! Work on the tasks given. Your result html will look like this:
>
> <img alt="preview-exercise-2-result" src="https://i.imgur.com/wbrtLNL.png" width="500">

## How does the web work?

### Client/Server architecture

![](assets/client-server.png)

A **Client** is the typical web user's internet-connected devices and apps. This can be a web browser, a Slack app, your phone, etc.

A **Server** is a computer or program that manages access to resources such as webpages, sites, or apps.

There are database servers, mail servers, game servers, etc. The vast majority of these servers are accessed over the internet. They can take the form of industrial server farms that provide a service to millions of users (used by Facebook, Google, etc.), to personal servers for storing your files.

The **server** communicates with **clients**.

Client–server systems use the **request–response** model: a client sends a request to the server, which performs some action and sends a response back to the client, typically with a result or acknowledgement.

![](assets/request-response-architecture.png)

### HTTP Requests

A server stores the data, and the client (other programs or computers) requests data or sends some of its own. But how do they talk to each other?

**For the client and the server to communicate they need an established language (a protocol)**. Which is what HTTP (Hypertext Transfer Protocol) is for. It defines the methods you can use to communicate with a server and indicate your desired actions on the resources of the server.

There are two main types of requests: **GET** and **POST**.

| Request type |                      Description                       |
| ------------ | :----------------------------------------------------: |
| GET          | Ask for a specified resource (e.g. show me that photo) |
| POST         |     Send content to the server (e.g. post a photo)     |

HTTP is the language of the internet. In our case we're using Javascript, but you can send HTTP requests with other languages as well.

### The Network Tab

The network tab is a useful tool that helps us understand how content is loaded on a website.

You can view it by `Right Click` > `Inspect` > `Network`.

Take some time to look at the network tab when we open [this lesson](https://syllabus.codeyourfuture.io/js-core-2/week-3/lesson.html)/

The important parts of the the Network Tab are:

- [Network Log](https://developers.google.com/web/tools/chrome-devtools/network#load)
- Timeline View
- [Resource Details](https://developers.google.com/web/tools/chrome-devtools/network#details)

#### Exercise - GET Requests

> Let's take a look at GET requests in the Browser.
>
> Look at this repository here:
>
> - https://github.com/CodeYourFuture/Network-Tab-Example
>
> In your groups, you should try to work out what you expect to see in the Network tab when we look at it. You should create a list of the requests that will be made in this format.
>
> **You are not allowed to open the website in a browser**
>
> e.g.
>
> 1. GET index.html
> 2. GET format.de
> 3. GET otherfile.se
> 4. ...
>
> When you have completed the list you should share it on Slack
>
> You can see the website online here
>
> - https://codeyourfuture.github.io/Network-Tab-Example/
>
> **Extra**
>
> Go to your favorite website and take a look at the Network tab. Can you work out what each (or any) of the requests are doing?
>
> Warning! There will be **a lot** of requests made on complicated websites.

#### Exercise - POST Requests

> Let's take a look at POST requests in the Browser.
>
> You can see the website online here
>
> - https://codeyourfuture.github.io/Network-Tab-Example/
>
> At the bottom of the page you will see a series of buttons. When you click a button on the website it will send a POST request to a server.
>
> 1. **Using only the Network tab** work out which button is sending a post request.
> 2. What is in the `body` of the post request?
>
> **Extra**
>
> 1. Did the `POST` request succeed?
> 2. Using the Details Panel, can you work out why?

{% include "./homework.md" %}

# JavaScript 2 Quiz

An optional quiz can be found [here](https://docs.google.com/forms/d/e/1FAIpQLSfMCZZkEWexs_7PbuRMpUPXqjjyXv814mhl3OikBv39QsqKSg/viewform) which can be used to test students understanding. This can be done in class or set as homework.
