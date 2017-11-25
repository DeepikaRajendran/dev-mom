---
layout: post
title: "AngularJS Removing the # in URLs"
modified: 2014-04-24 23:27:25 -0400
tags: [angularjs]
image:
  feature: 
  credit: 
  creditlink: 
comments: true
share: true
---
By default, AngularJS will route URLs with a hashtag.

For example:

* http://example.com/
* http://example.com/#/about
* http://example.com/#/contact


There are 2 things that need to be done to get clean URLs

* Configuring $locationProvider
* Setting our base for relative links
$location Service

### $locationProvider and html5Mode

We will use the $locationProvider module and set html5Mode to true on route definitions

{% highlight js %}

angular.module('myapp', [])
    
	.config(function($routeProvider, $locationProvider) {

		$routeProvider
			.when('/', {
				templateUrl : 'partials/home.html',
				controller : mainController
			})
			.when('/about', {
				templateUrl : 'partials/about.html',
				controller : mainController
			});

		$locationProvider.html5Mode(true);
	});

{% endhighlight %}
 

#### Setting base tag For Relative Links


We need to set base tag to the relative path.

{% highlight html %}

<!doctype html>
<html>
<head>
	<base href="/">
</head>

{% endhighlight %}
 
 