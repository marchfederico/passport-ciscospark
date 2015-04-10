# Passport-projectsquared

[Passport](https://github.com/march/passport) strategy for authenticating
with [Cisco's Project Squared](http://www.projectsquared.com/) using the OAuth 2.0 API.

This module lets you authenticate using Project Squared in your Node.js applications.  By
plugging into Passport, Project Squared authentication can be easily and unobtrusively
integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-projectsquared

## Usage

#### Configure Strategy

The ProjectSquared authentication strategy authenticates users using an ProjectSquared
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

The client ID and secret are obtained by registering an application at the
[Login with Project Square Developer Center](http://developer.projectsquared.com/).

    passport.use(new ProjectSquaredStrategy({
        clientID: PROJECTSQAURED_CLIENT_ID,
        clientSecret: PROJECTSQUARED_CLIENT_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/projectsquared/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ projectsquaredId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'projectsquared'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/projectsquared',
      passport.authenticate('projectsquared'));

    app.get('/auth/projectsquared/callback', 
      passport.authenticate('projectsquared', { failureRedirect: '/login' }),
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

