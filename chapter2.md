# Chapter 2 - Clipboard App

## Introduction

In this tutorial we will cover how to load and save data to a Personal Online Datastore (Pod).  The app is a simple web clipboard that allows you to save data to a store and then recover it later.

*What you will learn*

* How to set up [rdflib.js](https://github.com/linkeddata/rdflib.js/) to work with the web of data
* How to read data from a Pod
* How to write data to a Pod
* How to change the location of the URL you are using
* How to change query string to allow bookmarking

## The App

This app builds on the previous hello world app, which enables login and logout by introducing Personal Data Stores (Pods) and allowing read and write to those stores using [rdflib.js](https://github.com/linkeddata/rdflib.js/).  The app operates as a simple web clipboard that lets you save text to a location and retrieve it later.

The first thing that we will do is set up [rdflib.js](https://github.com/linkeddata/rdflib.js/).  It is sourced in to index.html

```html
    <script src="vendor/rdflib.min.js"></script>
```
    
After sourcing in the library, the first thing to do is to **initialize** a knowledge base graph, and a fetcher.  This is done using the `$rdf` global variables.

```javascript
    g = $rdf.graph();
    f = $rdf.fetcher(g);
```

The variable `g` will contain everything that is fetched using the fetcher, and also meta data about the documents that have been fetched.  The variable `f` can be used to fetch documents.

To see this in action we use the `nowOrWhenFetched` function of the fetcher to get data from  Pod.

Before we can do this we must determine the location from the query string or from a default as follows, using the angularJS search function:

```javascript
    var storageURI = 'https://clip.databox.me/Public/.clip/Public/test';
    if ($location.search().storageURI) {
      storageURI = $location.search().storageURI;
    }
```

For this app, the document is assumed to contain data of the form

```html
    <#this> <urn:tmp:clipboard> "data" .
```

The data above uses the turtle notation.  The `#this` subject is used to distinguish between document and data, and is similar to the 'this' keyword in JavaScript.  Best practice would be to mint an HTTP URI for the predicate, but for ease of demonstration purposes, a temporary URN is used at under the scheme urn:tmp:

Now we can fetch the data:

```javascript
    f.nowOrWhenFetched(storageURI, undefined, function(ok, body) {
      var clipboard = g.any($rdf.sym(storageURI + '#this'), TMP('clipboard'));
      $scope.clipboard = clipboard;
      $scope.storageURI = storageURI;
    });
```

The `nowOrWhenFetched` will call a callback either if the document is loaded in the graph, or once it is fetched from the web.  The `$rdf.sym` function simply changes a string into a URI by placing angle brackets around it.  We use the function `g.any` to get the object of the namespace TMP of value 'clipboard'

Once we have fetched this data we can set it to the screen, and also set the storageURI which has come back successfully.

To save the clipboard we issue a PUT request to the server. 

```javascript
    $http({
        method: 'PUT',
        url: $scope.storageURI,
        withCredentials: true,
        headers: {
            "Content-Type": "text/turtle"
        },
        data: '<#this> <urn:tmp:clipboard> """' + _clipboard + '""" .',
    }).
    success(function(data, status, headers) {
      $scope.notify('clipboard saved');
      $location.search('storageURI', $scope.storageURI);
    }).
    error(function(data, status, headers) {
      $scope.notify('could not save clipboard', 'error');
    });
```


More coming soon ...

## See Also

* [Source Code](https://github.com/melvincarvalho/clip)
* [Live Demo](http://melvincarvalho.github.io/clip/)
* [rdflib.js](https://github.com/linkeddata/rdflib.js/)