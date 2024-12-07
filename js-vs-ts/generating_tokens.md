## JS
```js
import jwt from "jsonwebtoken"
import { User } from "../models/user.model.js"

const generateTokens = (user) => {
	const accessToken = jwt.sign(
	{ id: user._id, email: user.email },
	process.env.ACCESS_TOKEN_SECRET,
	{ expiresIn: process.env.ACCESS_TOKEN_EXPIRY }
);

const refreshToken = jwt.sign(
	{ id: user._id, email: user.email },
	process.env.REFRESH_TOKEN_SECRET,
	{ expiresIn: process.env.REFRESH_TOKEN_EXPIRY }
);

return { accessToken, refreshToken };
};
```

## TS
```js
import jwt from "jsonwebtoken";
import dotenv from "dotenv";
import { IUser } from "../models/user.model.js";
import { User } from "../models/user.model.js";

// Define an interface for the user payload in the token
interface UserPayload {
	id: string;
	email: string;
}

// Type for the function that generates tokens
type GenerateTokensFunction = (user: IUser) => {
	accessToken: string;
	refreshToken: string
};

// Type for saving refresh token function
type SaveRefreshTokenFunction = (
	userId: string,
	refreshToken: string
) => Promise<IUser | null>;

// Type for verifying refresh token function
type VerifyRefreshTokenFunction = (
	refreshToken: string
) => Promise<IUser>;

// Ensure environment variables are loaded
dotenv.config();

// Function to generate tokens with explicit typing
const generateTokens: GenerateTokensFunction = (user) => {

// Safely assert environment variables (recommended to validate these exist)
const accessTokenSecret = process.env.ACCESS_TOKEN_SECRET;
const refreshTokenSecret = process.env.REFRESH_TOKEN_SECRET;
const accessTokenExpiry = process.env.ACCESS_TOKEN_EXPIRY;
const refreshTokenExpiry = process.env.REFRESH_TOKEN_EXPIRY;

// Validate environment variables
if (!accessTokenSecret || !refreshTokenSecret || !accessTokenExpiry || !refreshTokenExpiry) {
throw new Error('Missing JWT configuration environment variables');

}

  

// Generate access token

const accessToken = jwt.sign(

{ id: user._id, email: user.email } as UserPayload,

accessTokenSecret,

{ expiresIn: accessTokenExpiry }

);

  

// Generate refresh token

const refreshToken = jwt.sign(

{ id: user._id, email: user.email } as UserPayload,

refreshTokenSecret,

{ expiresIn: refreshTokenExpiry }

);

  

return { accessToken, refreshToken };

};

  

// Save refresh token to user document

const saveRefreshToken: SaveRefreshTokenFunction = async (userId, refreshToken) => {

return await User.findByIdAndUpdate(

userId,

{ refreshToken },

{ new: true }

);

};

  

// Verify refresh token

const verifyRefreshToken: VerifyRefreshTokenFunction = async (refreshToken) => {

// Ensure JWT_REFRESH_SECRET exists

const refreshTokenSecret = process.env.JWT_REFRESH_SECRET;

if (!refreshTokenSecret) {

throw new Error('JWT refresh secret is not defined');

}

  

try {

// Type assertion for decoded token

const decoded = jwt.verify(refreshToken, refreshTokenSecret) as UserPayload;

  

// Find user and verify refresh token

const user = await User.findById(decoded.id);

  

if (!user) {

throw new Error('User not found');

}

  

// Additional check for refresh token matching

if (user.refreshToken !== refreshToken) {

throw new Error('Invalid refresh token');

}

  

return user;

} catch (error) {

// Improve error handling

if (error instanceof jwt.TokenExpiredError) {

throw new Error('Refresh token expired');

}

if (error instanceof jwt.JsonWebTokenError) {

throw new Error('Invalid refresh token');

}

throw error;

}

};

  

export {

generateTokens,

saveRefreshToken,

verifyRefreshToken

};
```