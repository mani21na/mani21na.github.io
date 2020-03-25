---
layout: post
title:      "JavaScript asynchronous processing on Rails"
date:       2020-03-24 21:33:46 -0400
permalink:  javascript_asynchronous_processing_on_rails
---


**Synchronous vs Asynchronous**

The main difference between synchronous and asynchronous is how to have the order of execution.

Synchronization is a method in which the next operation is executed only when a request is received and a response is received. Asynchronous means that the next operation can be executed regardless of the response after sending the request.





**JavaScript is a single thread.**

JavaScript is a single thread language.
In other words, it is a language with only one call stack that handles events.
Therefore, if synchronous processing is performed when processing various events, a phenomenon occurs that no other task can be performed until all of them are processed.

Therefore, JavaScript sends events that cannot be processed immediately to the Web API, and when the call stack is empty, it first lists the events that have been processed and puts them back in the event queue. 

The order of entry into the Web API does not matter, but which event is processed first is important. Asynchronous with unclear execution order !!

But what if the order of asynchronous processing events becomes important?
For example, if you need to re-request profile picture information using the user's ID after asynchronous processing requesting the login user ID from the server.

There are several ways to handle asynchronous, which must be done sequentially.

1. Using callback functions
2. Promise
3. async / await using Promise





**Process data asynchronously using fetch() function and then method.**

Using fetch() function can be thought of as using API for performing your needs to return a response from a URI. The fetch() function retrieves data. It's a global method on the window object.

First, we'll provide a String, URL, argument to fetch(). You can paste this URL into a browser tab and see that this URL returns a JSON structure.

The then() takes a function. Here is where you tell JavaScript to ask the network response to be turned into JSON. 


```
fetch(URL)
.then(function(response) {
  return response.json();
})
.then(function(json) {
  console.log(json)
});
```





**Using rails for API-only applications**

Instead of using Rails to generate HTML that communicates with the server through forms and links, many developers are treating their web application as just an API client delivered as HTML with JavaScript that consumes a JSON API.

You can use multiple routes to differentiate between specific requests. In an API, these are typically referred to as endpoints. While working on your own API, you'll usually want to run your Rails server while trying various endpoints using fetch (). 

The Rails app is already running using the MVC structure. Run the rails server and visit the '/ route' path and you will see a list of data.

You are able to spin up the resources supported by the database and provide them in the browser. In other words, when a visitor navigates to '/ route' in this Rails app, the controller retrieves the data from the model and then displays that data in a view to serve to the visitor.

By using render json: in our Rails controller, we can take entire models or even collections of models, have Rails convert them to JSON, and send them out on request.

