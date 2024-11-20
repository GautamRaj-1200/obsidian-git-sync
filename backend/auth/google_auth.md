## Using Passport
1. Step - 1 : Get client Id and Secret from Google Developer Console
	- 
2. Step - 2 : configure passport
	- Required packages: `passport` and `passport-google-oauth2`
		- `import passport from "passport"`
		- `import OAuth2 from "passport-google-oauth2"`
		- `const OAuth2Strategy = OAuth2.Strategy;`
	- Create a function to configure passport with Google OAuth 2.0 strategy and handle user serialization and deserialization