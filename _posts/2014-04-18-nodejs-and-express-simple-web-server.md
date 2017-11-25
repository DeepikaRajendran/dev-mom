---
layout: post
title: "NodeJS and Express - Simple Web Server"
modified: 2014-04-18 10:57:23 -0400
tags: [nodejs,express, webserver]
image:
  feature: 
  credit: 
  creditlink: 
comments: true
share: true
---
In this post let's see how we can create a simple web server delivering static content with Node.js and and Express. 

But why Node.js instead of using Apache or IIS? To host the static files, for mobile web development or simple javascript library development, the nodejs express setup take less than 10 seconds.

#### Setup
{% highlight bash %}
$> npm install express
{% endhighlight %}

Create the web server:

{% highlight js %}
var express = require('express');
var app = express();
app.configure(function () {
    app.use(
        "/", //the URL throught which you want to access to you static content
        express.static(__dirname) //where your static content is located in your filesystem
    );
});

app.listen(3000); //the port you want to use
{% endhighlight %}

Execute your Web Server:
{% highlight bash %}
$> node server.js
{% endhighlight %}

Your web server is reachable through http://localhost:3000/