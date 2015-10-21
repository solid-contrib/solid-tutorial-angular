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

    ``` 
    <script src="vendor/rdflib.min.js"></script>
    ```
    
After sourcing in the library, the first thing to do is set up a knowledge base graph, and a fetcher.  This is done using the `$rdf` global variable

    ```javascript
    g = $rdf.graph();
    f = $rdf.fetcher(g);
    ```
    

More coming soon ...

## See Also

* [Source Code](https://github.com/melvincarvalho/clip)
* [Live Demo](http://melvincarvalho.github.io/clip/)
* [rdflib.js](https://github.com/linkeddata/rdflib.js/)