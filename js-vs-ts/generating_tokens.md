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
