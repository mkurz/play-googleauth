Play Google Auth Module
=======================

This module is a very simple implementation of OpenID Connect authentication
for Play 2 applications.

This has been extracted from the OpenID authentication support in Riff-Raff
at the same time that it has been migrated over from OpenID to OpenID Connect.

Versions
--------

For Play 2.2.x use version `0.0.5` (play2.2.x branch).

For later Play versions see the master branch of this project.

Adding to your application
--------------------------

In order to add Google authentication to your Play app you must:

 - get a set of API credentials for your app from the [Google Developer Console](https://console.developers.google.com)
 - ensure that you have switched on access to the `Google+ API` for your credentials
 - add play-googleauth to your libraryDependencies
 - create a GoogleAuthConfig instance with your API credentials and callback details (the callback must match both your
 app and the value you set in the developer console)
 - implement a login controller that has actions and routes for the login screen, login action, oauth callback and
 logout
 - implement a small trait that extends com.gu.googleauth.Actions and sets `loginTarget` to be the login action call
 - use `AuthAction` instead of `Action` to wrap actions in your controllers (these should be made
 available by extending the trait you implemented earlier

See the sample application to see how this is done.

Caveats
-------

This module brings in Apache Commons 1.9 which is later than the version Play requires by default. This is
usually fine as it is compatible.

The token acquired from Google is not cryptographically verified. This is not a problem as it is obtained directly
from Google over an SSL connection, used to authenticate the user and then thrown away. Do not keep the token around
and use it elsewhere unless this code is modified to carry out the verification.