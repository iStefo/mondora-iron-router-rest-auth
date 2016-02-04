[![Build Status](https://travis-ci.org/mondora/mondora-iron-router-rest-auth.svg?branch=master)](https://travis-ci.org/mondora/mondora-iron-router-rest-auth)
#mondora:iron-router-rest-auth

IronRouter plugin to (optionally) authenticate server routes.

## Install

```sh
meteor add mondora:iron-router-rest-auth
```

## How to

### Server-side

In your app somewhere, tell Iron Router to use the plugin:

```js
Router.plugin("restAuth");
```

Then, set up an HTTP route with Iron Router:

```js
Router.route("/my-route", {where: "server"})
    .get(function () {
        // this.user is either null or the authenticated user document
        // this.userId is either null or the authenticated user _id
    });
```

### Cient-side

Call your route passing the user's login token to authenticate:

```js
HTTP.get("/my-route?loginToken=userLoginToken", function (err, res) {
    // ...
});
```

You can either pass the token as url parameter (as shown above), or as a cookie called `loginToken`.

The `loginToken` is returned by the server upon a successful `login` ddp method call, and is stored by the client in
`localStorage["Meteor.loginToken"]`.
