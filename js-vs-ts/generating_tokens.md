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
import { User } from "../models/user.model.js";
import dotenv from "dotenv";

// Define an interface for the user payload
interface UserPayload {
    id: string;
    email: string;
}

// Define a function type with proper return type and parameter type
const generateTokens = (user: User): { accessToken: string; refreshToken: string } => {
    // Type assertion for environment variables
    const accessTokenSecret = process.env.ACCESS_TOKEN_SECRET as string;
    const refreshTokenSecret = process.env.REFRESH_TOKEN_SECRET as string;
    const accessTokenExpiry = process.env.ACCESS_TOKEN_EXPIRY as string;
    const refreshTokenExpiry = process.env.REFRESH_TOKEN_EXPIRY as string;

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

export { generateTokens };
```