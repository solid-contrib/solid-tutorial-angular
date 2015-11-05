# Chapter 4 - Solid Words

![](https://melvincarvalho.gitbooks.io/solid-tutorials/content/words.png)


## Introduction

In this tutorial we will expand the previous tutorial video into a real world useful app, one for word training and vocabulary.

*What you will learn*

* How to structure JavaScript in several parts
* How to set up a turtle data file on github
* How to use localStorage to save state
* How to automatically remember a user and login
* How to prepare language files to be used in vocab training
* How to add audio to apps

## The App


The next tutorial is an app that is used to learn vocabulary in a foreign language.  A file is prepared containing the 10,000 most common words in a target language.  The source for word frequency was [wictionary](https://en.wiktionary.org/wiki/Wiktionary:Frequency_lists).  For this demo I have used the czech language with english, but any language pair is possible.

The app will test you randomly on the 1000 most common words.  You can click on the word if you dont know it and a translation will momentarily appear.  If you know the word you can click 'easy' if you dont know the word, click 'again', and if you almost know it, click 'good'.  This is a typical style for [Spaced Repitition](https://en.wikipedia.org/wiki/Spaced_repetition) style memory learning.

The number of words can be cycled to 2000, 3000, 5000 or 10000 as you progress using the changer on the left.  Or an arbitrary number can be tested using the max query string parameter.  Displayed next to the graph is how difficult the word is in terms of frequency.  As you make more trials the number of words increases and your percentage right.  It is possible to reset the number by tapping it.

From a list of words it's possible to paste it into an online translator and get a list of translations.  For this I used google translate.  A simple program can change a 2 column text file into the needed turtle.  I used awk for this

``` 
awk -F $'\t' ' { print "<#" ++i "> <http://www.w3.org/2000/01/rdf-schema#label>" " \""  $2 "\"" "@en .\n" "<#" i ">  <http://www.w3.org/2000/01/rdf-schema#label>" " \""  $1 "\"" "@cs ." }'
```

Which should give you output something a bit like this:

```html
    <#1512> <http://www.w3.org/2000/01/rdf-schema#label> "žádost"@cs .
    <#1512> <http://www.w3.org/2000/01/rdf-schema#label> "application"@en .
````

One line is in Czech (cs) one in English (en).  This file can be conveniently stored as a .ttl in gh-pages on github so that it can be [loaded](https://github.com/melvincarvalho/data/blob/master/vocab/czech.ttl) into the app dynamically.  This is a great way to host all sorts of linked data content.

A number of things are persisted in localStorage.  The word totals in each bucket (easy, good and again), your user id, and the word lists.  This is used to log you in automatically on future usage of the app

```JavaScript
    if (localStorage.getItem('user')) {
      var user = JSON.parse(localStorage.getItem('user'));
      $scope.loginSuccess(user);
    }
```

The app is divided into sections for init, auth, fetching, rendering and helper functions.  This will be a typical division of functions for more complex apps.

Audio has also bee added to the buttons using the [ngAudio](https://danielstern.github.io/ngAudio/#/) function and a simple tag in the html

````html
   "ng-audio="audio/button-3.mp3"
```

Putting these pieces together creates a complete and quite useful Solid application.

  [Live Demo](http://melvincarvalho.github.io/vocab/)
  
While the english czech language pair was used as default any word file could be used for vocabulary testing.

## Summary


## See Also

* [Source Code](https://github.com/melvincarvalho/vocab/)
* [Live Demo](http://melvincarvalho.github.io/vocab/)
* [wictionary](https://en.wiktionary.org/wiki/Wiktionary:Frequency_lists)
* [Spaced Repitition](https://en.wikipedia.org/wiki/Spaced_repetition)
* [ngAudio](https://danielstern.github.io/ngAudio/#/)
