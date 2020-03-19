---
layout: post
title:      "First Js Project"
date:       2020-03-19 04:31:56 +0000
permalink:  first_js_project
---


I would like to summarize the difficulties and learning I have experienced while working on this project.

It feels a bit familiar with **Callback** and **Promise** that were considered unfamiliar and felt like they were in the air.

**Why use callbacks**

In most cases, We are creating programs and applications that work synchronously. In other words, some tasks only start after the previous one has completed.  Often when we request data from other sources, such as an external API, we don’t always know when our data will be served back. In these instances, we want to wait for the response, but we don’t always want our entire application grinding to a halt while our data is being fetched. These situations are where callback functions come in handy.



**Why use promises**

In single-threaded JavaScript, callbacks have been used for asynchronous processing.
Thanks to this, the asynchronous processing could be done completely, but the disadvantages were revealed as the number of such callbacks was increased.
The disadvantages are that when asynchronous processing needs to be executed sequentially, asynchronous processing is superimposed, so that errors and exception processing are difficult and complexity due to overlapping increases.
In order to solve these two shortcomings, Promise has been created as a library from the past, and ES6 supports it at the language level.


