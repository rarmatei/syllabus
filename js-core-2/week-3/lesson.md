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
- Understand the difference between a GET and POST request
- Understand how resources are loaded on the internet using GET and POST
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

#### Exercise (1)

> - Using setTimeout, change the background colour of the page after 5 seconds (5000 milliseconds).
> - Update your code to make the colour change _every_ 5 seconds to something different. Hint: try searching for `setInterval`.
>
> ![](http://g.recordit.co/g2EqBccNzh.gif)
>
> Complete the exercises in this [CodePen](https://codepen.io/makanti/pen/abOreLg?editors=1011)

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

HTTP is the language of the internet. In our case we're using Javascript, but you can send HTTP requests with other laguages as well.

#### Exercise (2)

> Complete the exercises in this [CodePen](https://codepen.io/textbook/pen/MWwMgmW?editors)
>
> - You are given a list of movie objects to work with<br/>
> - Use setTimeout to imitate that some actions take time
> - Remember that setTimeout behaves asynchronously
>
> All set, go! Work on the tasks given. Your result html will look like this:
>
> <img alt="preview-exercise-2-result" src="https://i.imgur.com/wbrtLNL.png" width="500">

{% include "./homework.md" %}
