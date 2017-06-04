## AJAX Requests and APIs

---

**AJAX** - Asynchrous JavaScript And XML request

An asynchronous request can be fired off **at any time** (before or after a page has loaded) and the response to an asynchronous request often includes HTML that can be dynamically inserted into a page.

---

### Client Server Demonstration

**GET Request:** An internet request for data. Sent from a client to a server.

**Response:** A server's response to a request. Sent from a server to a client. A response to a GET request will usually include data that the client needs to load the page's content.

---

## Necessary Components Of An AJAX Request

You only need a URL for an AJAX request.
jQuery.ajax( url [, settings ] ) // all settings are optional
[link](http://api.jquery.com/jquery.ajax/)

---

## API's

[Google's APIs / All the Google services you can imagine.](https://developers.google.com/apis-explorer/#p/)

[Giant database of APIs](https://www.programmableweb.com/apis/directory)

---

## jQuery - $jQuery

$Dollar, Baby!

1. [jQuery.ajax()](http://api.jquery.com/jquery.ajax/)
1. [jQuery.getJSON()](http://api.jquery.com/jquery.getjson/)

---

### Building the Move Planner app

1. [The NYT article search API](http://developer.nytimes.com/article_search_v2.json)
1. [NYT Implementation Project](https://laurahesse.github.io/NYT-Implementation/)
1. [NYT Implementation Project Repo](https://github.com/LauraHesse/NYT-Implementation)

--

### .fail()

`.fail()` goes into effect if Ajax request fails. Requests go wrong! It's awesome that you've got error handling in place.

```
.fail(function(err) {
  $nytHeaderElem.text('New York Times Articles could not be loaded');
});
```
---

## Cross-Origin Resource Sharing ([CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing))

CORS works around a sometimes overly-strict browser policy meant to protect servers from malicious requests. CORS is enabled on the server-side, so you won't generally need to worry about it for your code. You do need to know about it though, since some APIs support it, and some do not.

### What is CORS and why are we using it?

CORS works around the same-origin policy. The same-origin policy was implemented by web browsers to prevent malicious scripts from untrusted domains from running on a website. In other words, it ensures sure that scripts from one website can't insert themselves into another.

For example, the same-origin policy keeps the bad guys’ JavaScript from somehow running on your bank’s website and stealing your information.

Over time, developers realized that this policy was too strict, and often got in the way of legitimate use-cases. There are many reasons to serve content from multiple domain origins, and so developers found a way around it.

Developers that maintain server-side APIs can enable CORS on their servers to disable the same-origin policy. CORS is a relatively recent feature added to browsers. When certain headers are returned by the the server, the browser will allow the cross-domain request to occur.

For APIs that don't support CORS, you may need to use another method. The other way around the same-origin policy is JSON-P. JSON-P is a unique trick to allow cross-domain requests. Many APIs allow you to provide a callback function name, and they will generate a JavaScript file that passes the data into that function when it gets run in your browser.

This isn't the simplest thing to implement cleanly, but if you're using jQuery to create your AJAX requests, using JSON-P is as simple as adding an extra property to the options object that you pass into the AJAX method. You'll be doing this very soon, and I promise it's not as scary as it sounds. :)

### The nitty gritty of JSON-P

Your application loads up a script from the other domain using a simple `<script>` tag. Once the script has been received, that code gets run by your browser. All the code does is build the data object you requested as a simple JavaScript object, and runs the callback function (that you told the server to use) with the object (your data) as a parameter.

You’ll need to refer to the documentation for any data API’s you want to use, and figure out if the API supports CORS or if you need to use JSON-P.
---

## Quiz: Wikipedia API

[jQuery.ajax()](http://api.jquery.com/jquery.ajax/)
```
$.ajax({
url: wikiLink,
dataType: "jsonp",
//jsonp: "callback",
}).done(function(response) {
    var articleList = response[1];

    for (var i = 0 ; i < articleList.length; i++) {
        articleStr = articleList[i];
        var url = "http://en.wikipedia.org/wiki/" + articleStr;
        $wikiElem.append('<li><a href="' + url + '">' + articleStr + "</a></li>");
    }
});
```

## MVO - Model, View and Octopus


## Code organization techniques !!!

Refactoring "code" is the process by which you take a piece of code and make it more readable or maintainable without changing it's functionality.  Break up large functions or complicated functions so its easier to access from the outside world.

Increase readability, maintainability and ease of working with your code.

### Using an organization library

MVO - Model View Octopus :)
Separate concerns, minimize connections.

Use Libraries and use Frameworks. Write and re-use code.
jQuery has a great Library for AJAX, DOM Manipulation and much more.

Library - bunch of code that someone wrote that we could use.
Organizational Libraries - focus on application organization.

### Fundamental organizational Concepts

MODELS - represent your DATA.
COLLECTIONS - Smart ARRAYS filled with smart information.
MODEL COLLECTION - collections of data.

ViewModel, Controller or Octopus - connects and separates Model from the View.

VIEWS - draw the interface, allow the user to interact with the interface.

## [Knockout JS](http://knockoutjs.com/) - Model, View, ViewModel(Octopus)

1. ViewModel - Similar to Octopus
1. Declarative Bindings - Connect View & ViewModel
1. Automatic UI Refresh - Automatic refresh the view.
1. Updates the View automatically when the model changes.
1. Dependency Tracking - Models can depend on other models.

[Knockout JS example](http://jsfiddle.net/rniemeyer/3Lqsx/)

```
HTML
<div>You've clicked <span data-bind='text: numberOfClicks'>&nbsp;</span> times</div>

JS
this.numberOfClicks = ko.observable(0);
```

Knockout handles Models little bit differently, instead of storing data in a plain old OBJECT or as a simple value, knockout stores it a special Knockout Object ```var myNum = ko.observable(5);```

### Documentation - Love it, Hate it.. you really need it!

[Knockout example here](https://github.com/LauraHesse/ud989-cat-clicker-ko-starter)

### Computed Observables

Instead of storing as a String, store it as a function
```
firstName = "Ben"
lastName = "Jaffe"
fullName = function(){
    return firstName + " " + lastName;
}

```

---
**MODELS**

1. Observables
1. Computed Observables
1. Observable Arrays

**ViewModel**

**View**

1. Bindings (data-bind="")
