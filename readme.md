# Passport.js authentication for Earthmaps

[Passport](http://passportjs.org/) strategy for authenticating with [Earthmaps](http://earthmaps.org/) using the OAuth 2.0 API.

This module lets you authenticate using Earthmaps in your Node.js applications.

By plugging into Passport, Earthmaps authentication can be easily and unobtrusively integrated into any application or framework that supports [Connect](http://www.senchalabs.org/connect/)-style middleware, including [Express](http://expressjs.com/).

## Install
```
npm install passport-earthmaps
```

## Usage

#### Configure Strategy

The Earthmaps authentication strategy authenticates users using a Earthmaps account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts these credentials and calls `done` providing a user, as well as `options` specifying a client ID, client secret, and callback URL.
```
var OAuth2Strategy = require("passport-earthmaps").Strategy;

passport.use(new OAuth2Strategy({
	clientID: CLIENT_ID,
	clientSecret: CLIENT_SECRET,
	callbackURL: "http://www.example.net/auth/earthmaps/callback"
	},
	function(accessToken, refreshToken, profile, done) {
	User.findOrCreate({ providerId: profile.id }, function (err, user) {
		return done(err, user);
	});
	}
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'earthmaps'` strategy, to authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/) application:

```
app.get('/auth/earthmaps',
	passport.authenticate('earthmaps'));

app.get('/auth/earthmaps/callback',
	passport.authenticate('earthmaps', { failureRedirect: '/login' }),
	function(req, res) {
	// Successful authentication, redirect home.
	res.redirect('/');
	});
```

## Credits

Initiated by [Makis Tracend](http://github.com/tracend)

Part of [Earthmaps](http://earthmaps.org/) by [K&D Interactive](http://kdi.co/)

Released under the [MIT license](http://makesites.org/licenses/MIT)

