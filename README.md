# Passport-ciscospark

[Passport](https://github.com/march/passport) strategy for authenticating
with [Cisco Spark](http://www.ciscospark.com/) using the OAuth 2.0 API.

This module lets you authenticate using Cisco Spark in your Node.js applications.  By
plugging into Passport,Cisco Spark authentication can be easily and unobtrusively
integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-ciscospark

## Usage

#### Configure Strategy

The Cisco Spark authentication strategy authenticates users using an Cisco Spark
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

The client ID and secret are obtained by registering an application at DevNet
[Login  to the Cisco Developer Center](http://developer.cisco.com/).

    passport.use(new CiscoSparkStrategy({
        clientID: CISCOSPARK_CLIENT_ID,
        clientSecret: CISCOSPARK_CLIENT_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/ciscospark/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ ciscosparkId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'ciscospark'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/ciscospark',
      passport.authenticate('ciscospark'));

    app.get('/auth/ciscospark/callback', 
      passport.authenticate('ciscospark', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });



## Tests

    $ npm install --dev
    $ make test


## Credits

  - [Marcello Federico](http://github.com/marchfederico)
  
## Thanks

  - [Jared Hanson](http://github.com/jaredhanson)


## License

[The MIT License](http://opensource.org/licenses/MIT)

