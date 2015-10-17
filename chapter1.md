# Chapter 1 - Hello World

## Introduction

In this tutorial we will cover how to build a simple hello world app using the SoLiD framework.  What you will learn may include:

* How to create your first SoLiD app
* How to use decentralized login
* How to to delegate HEAD requests to get a User: header
* How to logout
* How to use notifcations using lumx and AngularJS

## The App

Hello world is a simple app that allows decentralized login and logout using the [WebID](http://webid.info/) Identity system.

The **login** code is below:

```javascript
    $http({
      method: 'HEAD',
      url: AUTHENDPOINT,
      withCredentials: true
    }).success(function(data, status, headers) {
      var user = headers('User');
      if (user && user.length > 0 && user.slice(0,4) == 'http') {
        LxNotificationService.success('Login Successful!');
        $scope.loggedIn = true;
        $scope.user = user;
      } else {
        LxNotificationService.error('WebID-TLS authentication failed.');
        console.log('WebID-TLS authentication failed.');
      }
      $scope.loginTLSButtonText = 'Login';
    }).error(function(data, status, headers) {
      LxNotificationService.error('Could not connect to auth server: HTTP '+status);
      console.log('Could not connect to auth server: HTTP '+status);
      $scope.loginTLSButtonText = 'Login';
    });

  ```
  
The system used is a delegated authentication.  This is because a server is required in order to verify who a user is.

A HEAD request to any WebID enabled server will return a User: header telling who is using the app.  That user can then be used to cusomize the app.  In our case we simply set `$scope.user`.

The withCredentials flag is set to true in order to prevent a CORS error.

The AUTHENDPOINT in our example is set to : https://databox.me/

```javascript
    AUTHENDPOINT = "https://databox.me/";
```

The **logout** code simply unsets the `$scope.loggedIn` variable:

```javascript
  $scope.logout = function() {
    LxNotificationService.success('Logout Successful!');
    $scope.loggedIn = false;
  };
```

Putting this simple functionality together in using the [AngularJS](https://angularjs.org/) framework (with [lumx](http://ui.lumapps.com/) extensions) it is possible to create a simple demo:

  [Live Demo](http://melvincarvalho.github.io/helloworld/)
  
## Summary

In this chapter we have shown how to identify and verify a user using delegated login and WebID.  We have packaged the code into an [AngularJS](https://angularjs.org/) app and presented a simple demo.  In the next chapter we will show how to save data to your Personal Online Data Store (Pod).

## See Also

* [Source Code](https://github.com/melvincarvalho/helloworld)
* [Live Demo](http://melvincarvalho.github.io/helloworld/)
* [WebID](http://webid.info/)
* [AngularJS](https://angularjs.org/)
* [Lumx](http://ui.lumapps.com/)
