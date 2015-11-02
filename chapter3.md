# Chapter 3 - Video App

## Introduction

In this tutorial we will cover how to load and save data video links to a Personal Online Datastore (Pod) and display it on screen.  A slightly more sophisticated UI will also be used.

*What you will learn*

* How to read and write video URLs to a Pod
* How to embed video in a page
* How to add a sidebar
* How to add a menu bar
* How to display modal dialogs
* How to add a DOAP project file


## The App

The video app follows the model of the previous clipboard app but adds a few more features to the UI and allows embedding of a video element via an iframe.  A demo and the source code can be found in the footnotes.

The data format used for storing a video in a file here is:

```
    <#this> <http://rdfs.org/sioc/ns#content> "content" .
```

The predicate here is an HTTP URI that uses the [SIOC](http://rdfs.org/sioc/spec/) vocabulary.  In this case the content is an embeddable video URL (as a string).  This is fetched after login using the code:

```JavaScript
  $scope.fetchVideo = function() {
    f.nowOrWhenFetched($scope.storageURI, undefined, function(ok, body) {
      var video = g.any($rdf.sym($scope.storageURI + '#this'), SIOC('content'));
      $scope.setVideo(video);
    });
  };
```

The setVideo function simply embeds the video file in an iframe element after determining the width and height (for mobile optimization).

```JavaScript
    var height = Math.round(( width * 3 ) / 4);
    var iframe = '<iframe width="' + width + '" height="' + height +
                 '" src="'+uri+'"></iframe>';
    $('#video').empty().append(iframe);
```


More Coming soon ...

## See Also

* [Source Code](https://github.com/melvincarvalho/video)
* [Live Demo](http://melvincarvalho.github.io/video/)
* [SIOC](http://rdfs.org/sioc/spec/)
