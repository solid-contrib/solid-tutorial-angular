# Chapter 1 - Hello World

Hello world is a simple app that allows decentralized login and logout using the WebID Identity system.

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