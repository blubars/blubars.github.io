---
layout: post
title: "Learning AngularJS"
date: 2014-11-23 18:37
categories: blog
tags: coding javascript web angularjs
---
Documenting my attempts to learn AngularJS. I know almost no javascript. I've focused on C/embedded programming mostly, with some python and Java, but no Javascript. When I was in high school, I used to mess around with static HTML/CSS web pages with niblets of javascript thrown in for spice. In college, messed around a little more with manipulating the DOM using javascript, but never did anything meaningful, and I have since forgotten. So I'm effectively starting from scratch here.

Using [egghead.io](https://egghead.io/articles/new-to-angularjs-start-learning-here).

Note: JQuery Lite is also included with AngularJS.

## Step One: "installing" AngularJS
* Add Angular script
  * Instead of downloading angular and including it on the web server, recommended to source it directly from google's CDN: [angularjs.org](http://www.angularjs.org) has a link to it under Download.
  * I will be using <del>1.3.x (latest version)</del>1.2.x since it is what the tutorials use
* Initialize the app with ng-app
  1. Add <code>ng-app</code> to the html tag
  2. Bind h1 tag to a "property" called hello: <code><h1>&#123;&#123;hello&#125;&#125;</h1></code>
  3. Add input field with <code>ng-model="hello"</code>. This way, whatever is entered in the input field will update the h1 tag.
* Simple two-way binding with ng-model

{% highlight html %}
{% raw %}
<!DOCTYPE html>
<html ng-app>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
  </head>
  <body>
    <h1>{{hello}}</h1>
    <input type="text" ng-model="hello" />
  </body>
  <script type="text/javascript" 
          src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.3/angular.min.js">
  </script>
</html>
{% endraw %}
{% endhighlight %}

## Step Two: Two-way Binding
Binding is a mechanism for tying your HTML to your data, via &#123;&#123;expressions&#125;&#125;. Many expressions can be evaulated within the curly braces, but should be kept to a minumum. Very useful for creating input and giving users a way to interact with the site. Lets you manipulate a LARGE part of the DOM... not just text, but element classes, for example.

## Step 3: Controllers
Controllers connect the markup with the data. <code><div ng-controller="FirstCtrl"></code> Provides the data that the data bindings will use. Everything inside that div will have the "$scope" of that controller. The controller can modify the scope. e.g. <code>$scope.data = {message: "Hello"};</code>
Global controller functions are apparently no longer enabled by default in 1.3. So I'm reverting back to 1.2 to learn.

## Step 4: Sharing Data Between Controllers
First, the example shows how if there's a parent scope, both children can inherit from it. But there's a better way... creating a service. This is done with a factory. After you have a service which in this case the service is called Data and it returns an object with the string), you can share it with the controllers.

{% highlight javascript %}
// myApp should be the name of ng-app in the html
var myApp = angular.module('myApp', []);
myApp.factory('Data', function() {
  return {message: "I'm data from a service"}
})

function FirstCtrl($scope, Data) {
  $scope.data = Data;
}
function SecondCtrl($scope, Data) {
  $scope.data = Data;
}
{% endhighlight %}

## Step 5: Defining a Method on the Scope
Defining a methon on the scope of the controller is pretty easy. Just define a function inside the controller, like thus:
{% highlight javascript %}
function FirstCtrl($scope, Data) {
  $scope.data = Data;
  $scope.reversedMessage = function() {
    return $scope.data.message.split("").reverse().join();
  }
  $scope.reversedMessageBetter = function(message) {
    return message.split("").reverse().join();
  }
}
{% endhighlight %}

If any of the scope models change, this method will be invoked automatically on the new scope.

## Step 6: Filters
Apparently the method from step 5 is the perfect use case for a filter. Filters let you create reusable text-manipulating functionality in an easy syntax. So let's turn it into one. 

You can add a filter to the App, for example the reverse filter would be:
{% highlight javascript %}
myApp.filter('reverse', function() {
  return function(text) {
    return text.split("").reverse().join("");
  }
})
{% endhighlight %}

...and then in the html, you would use it like this:
{% highlight html %}
<div ng-app="myApp">
  <div ng-controller="FirstCtrl">
    <input type="text" ng-model="data.message" />
    <h1>&#123;&#123;data.message|reverse&#125;&#125;</h1>
  </div>
</div>
{% endhighlight %}

## Step 7: ng-repeat
The ng-repeat directive lets you repeat the same UI element over and over with each value from objects in a set. For example, generate a table from a list of actors and their roles:
{% highlight html %}
{% raw %}
<div ng-controller="AvengersCtrl">
  <input type="text" ng-model="search.$">
  <table>
    <tr ng-repeat="actor in avengers.cast|filter:search">
      <td>{{actor.name}}</td>
      <td>{{actor.character}}</td>
    </tr>
  </table>
</div>
{% endraw %}
{% endhighlight %}

### Other built-in filters: 
* filter:search
* orderBy:'name'
* orderBy:-'name' -- order in reverse
* limitTo:-5 -- show last 5 results
* orderBy:'name'|limitTo:5|filter:search -- show first 5 results alphabetically
* lowercase, uppercase

## Step 8: Directives
According to egghead.io, "The killer feature. That said, they are aguably the steepest cliff...". Directives let you create HTML elements, attributes, and classes.
e.g.:
{% highlight javascript %}
var app = angular.module("superhero", [])
app.directive("superman", function() {
  return {
    restrict: "E",
    template: "<div>Here I am to save the day</div>"
  }
})
{% endhighlight %}
{% highlight html %}
<div ng-app="superhero">
  <superman></superman>
</div>
{% endhighlight %}

What does this render?
  Here I am to save the day
Cool.

You can also access the scope, element, and attributes from the directive. For example if you want to print "Hello world" using a line like this:
<code><div my-first-directive="" message="world"></div></code>:
{% highlight javascript %}
egghead.controller("AppCtrl", function() {
  var app = this;
  app.message = "Hello";
}
egghead.directive("myFirstDirective", function() {
  return function(scope, element, attrs) {
    element.text(scope.app.message + " " + attrs.message);
  }
})
{% endhighlight %}

Caveat: can do this more easily with a template in the directive, and typically want to avoid scope inheritance like this.

## Step 9: Directives and Custom Behaviors
You can also use directives to set up some behaviors. This is the recommended way of interacting with the DOM. Shortcut: if all you're going to do is use the link function in the directive object, you can just have the directive return a function(scope, element).
{% highlight javascript %}
app.directive("enter", function() {
  return function(scope, element) {
    element.bind("mouseenter", function() {
      console.log("I'm inside of you!");
    )}
  }
})
{% endhighlight %}

## Step 10:
Using directives to add/remove a class:
{% highlight javascript %}
app.directive("enter", function() {
  return function(scope, element, attrs) {
    element.bind("mouseenter", function() {
      element.addClass(attrs.enter);
    })
  }
})
app.directive("leave", function() {
  return function(scope, element, attrs) {
    element.bind("mouseleave", function() {
      element.removeClass(attrs.enter);
    })
  }
})
{% endhighlight %}
...and the HTML:
<code><div enter="panel" leave>I'm content!</div></code>

## Step 11: Isolated Scope
Directives need isolated scope for many meaningful behavior. The syntax is confusing me at the moment. I think I'll resume this at a later date.
