## Using Passport
1. Step - 1 : Get client Id and Secret from Google Developer Console
	- 
2. Step - 2 : configure passport
	- Required packages: `passport` and `passport-google-oauth2`
		- `import passport from "passport"`
		- `import OAuth2 from "passport-google-oauth2"`
		- `const OAuth2Strategy = OAuth2.Strategy;`
	- Create a function to configure passport with Google OAuth 2.0 strategy and handle user serialization and deserialization
		- Initialize the OAuth2 strategy:
			- Accept `clientID`, `clientSecret`,`callbackURL` and `scope`
			- Define a callback function to handle the logic after Google returns the user's profile data.
		- Callback Function execution
			- Input `accessToken`,`refreshToken`, `profile` and `done`
		- Fetch or create user
			- Attempt to find an existing user in the database based on `profile.id`:
				- Call `User.findOne` with `{ googleId: profile.id }`.
		- **Check if the User Exists:**
		- **Case 1**: User exists:
		    - Retrieve the user and pass it to the `done` function.
		- **Case 2**: User does not exist:
		    - Create a new user object:
		        - Assign `googleId` to `profile.id`.
		        - Assign `displayName` to `profile.displayName`.
		        - Assign `email` to the first email in `profile.emails[0].value`.
		        - Assign `image` to the first profile picture URL in `profile.photos[0].value`.
		    - Save the new user to the database using `user.save()`.