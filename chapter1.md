# Chapter 1 - Solid Hello

## Introduction

In this tutorial we will cover how to build a simple client side hello world app using the [Solid](https://github.com/solid) framework.  

*What you will learn*

* How to create your first client side [Solid](https://github.com/solid) app
* How to use decentralized login and logout
* How to delegate HEAD requests to identify using the [User](https://www.w3.org/community/rww/wiki/User_Header) header
* How to use notifcations using [Lumx](http://ui.lumapps.com/) and [AngularJS](https://angularjs.org/)

## The App

[Solid](https://github.com/solid) apps typically run client side and do not require a server, except to identify a user, or store data.

This app written using on [AngularJS](https://angularjs.org/).  Setup and scaffolding of the app is out of scope for this tutorial.  But there are many [guides](https://docs.angularjs.org/misc/started) online that show you how to get started.  The code is also available for download in the footnotes.

Hello world is a simple app that allows decentralized login and logout using the [WebID](http://webid.info/) Identity system.  A remote server will perform the authentication, typically using TLS, but any authentication method is allowed provided that the [User](https://www.w3.org/community/rww/wiki/User_Header) header is sent back.


First, we will look at how to use decentralized login using JavaScript.  Using [WebID](http://webid.info/) it is possible to login using an HTTP URI that denotes you as person, and that can also be dereferenced to find out more about you.  In this app, we will simply get the URI of the user and display it on screen.  The **login** code is below:

```javascript
    $http({
      method: 'HEAD',
      url: AUTHENDPOINT,
      withCredentials: true
    }).success(function(data, status, headers) {
      var header = 'User';
      var scheme = 'http';
      var user = headers(header);
      if (user && user.length > 0 && user.slice(0,scheme.length) === scheme) {
        $scope.notify('Login Successful!');
        $scope.loggedIn = true;
        $scope.user = user;
      } else {
        $scope.notify('WebID-TLS authentication failed.', 'error');
      }
      $scope.loginTLSButtonText = 'Login';
    }).error(function(data, status, headers) {
      $scope.notify('Could not connect to auth server: HTTP '+status);
      $scope.loginTLSButtonText = 'Login';
    });


  ```
  
The system used is a delegated authentication.  What that means is that we use a server to identify and verify who is using the app.  This is because a server is required in order to verify who a user is.  

The AUTHENDPOINT in our example is set to : https://databox.me/

```javascript
    AUTHENDPOINT = "https://databox.me/";
```
The withCredentials flag is set to true in order to prevent a CORS error.

A HEAD request to any WebID enabled server will return a User: header telling who is using the app.  That user can then be used to customize the app.  In our case we simply set `$scope.user`.  This is enough to login to our simple app, and display a hello world message.

The **logout** code simply unsets the `$scope.loggedIn` variable, and returns you to the start screen:

```javascript
  $scope.logout = function() {
    $scope.init();
    $scope.notify('Logout Successful!');
  };
```

Putting this simple functionality together in using the [AngularJS](https://angularjs.org/) framework (with [lumx](http://ui.lumapps.com/) extensions) it is possible to create a simple demo:

  [Live Demo](http://melvincarvalho.github.io/helloworld/)
  
The `$scope.notify` function returns a message to the user to tell them they have logged in or out.  This completes the functionality of this simple app.
  
## Summary

In this chapter we have shown how to identify and verify a user using delegated login and WebID.  We have packaged the code into an [AngularJS](https://angularjs.org/) app and presented a simple demo.  In the next chapter we will show how to save data to your Personal Online Datastore (Pod).

## See Also

* [Source Code](https://github.com/melvincarvalho/helloworld)
* [Live Demo](http://melvincarvalho.github.io/helloworld/)
* [Solid](https://github.com/solid)
* [WebID](http://webid.info/)
* [AngularJS](https://angularjs.org/)
* [Lumx](http://ui.lumapps.com/)
* [User Header](https://www.w3.org/community/rww/wiki/User_Header)