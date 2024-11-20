## Using Passport
1. Step - 1 : Get client Id and Secret from Google Developer Console
2. Step - 2 : configure passport
	- Required packages: `passport` and `passport-google-oauth2`
		- `import passport from "passport"`
		- `import OAuth2 from "passport-google-oauth2"`
		- `const OAuth2Strategy = OAuth2.Strategy;`
	- Create a function to configure passport with Google OAuth 2.0 strategy and handle user serialization and deserialization
		1. Initialize OAuth2 Strategy with client credentials, callback URL and scope.
		2. Define the callback function:
	    Input: accessToken, refreshToken, profile, done.
		3. Attempt to find a user:
		    user = User.findOne({ googleId: profile.id })
		4. If user exists:
		    Call done(null, user)
		5. If user does not exist:
		    Create a new user object:
		        googleId = profile.id
		        displayName = profile.displayName
		        email = profile.emails[0].value
		        image = profile.photos[0].value
		    Save the user to the database.
		    Call done(null, user)
		6. Handle errors:
		    If an error occurs, call done(error, null).
