# Passport-Hatena
===============

[Passport](http://passportjs.org/) strategy for authenticating with [Hatena](http://www.hatena.ne.jp/) using the OAuth 1.0a API

This module can be used with passport in Node.js.
You can integrate into below applications or frameworks.
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-hatena-oauth

## Usage

### Configuration Strategy

This Hatena passport module requires your application' id. 
You can get this id from [Hatena Developer Center](http://developer.hatena.ne.jp/ja/documents/auth/apis/oauth)

### Authorization Endpoint

    passport.use(new HatenaStrategy({
        consumerKey: HATENA_CONSUMER_KEY,
        consumerSecret: HATENA_SECRET_KEY,
        callbackURL: "http://127.0.0.1:3000/auth/hatena/callback"
      },
      function(token, tokenSecret, profile, done) {
        User.findOrCreate({ hatenaId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'hatena'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/hatena',
      passport.authenticate('hatena'), { scope: ['read_public'] });
    
    app.get('/auth/hatena/callback',
      passport.authenticate('hatena', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

### License

[The MIT License](http://opensource.org/licenses/MIT)

