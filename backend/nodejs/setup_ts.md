## Install
- `npm i bcrypt cookie-parser cors dotenv express jsonwebtoken mongoose nodemailer`
- `npm i -D prettier nodemon rimraf @types/bcrypt @types/cookie-parser @types/cors @types/dotenv @types/express @types/jsonwebtoken @types/node @types/mongoose`
## `app.ts`

```js
import express from "express"
import cors from "cors"
import cookieParser from "cookie-parser"
const app = express()

app.use(cors({
	origin: process.env.CORS_ORIGIN,	
	credentials: true,
}))

app.use(express.json({ limit: "16kb" }))
app.use(express.urlencoded({ extended: true, limit: "16kb" }))
app.use(express.static("public"))
app.use(cookieParser()) 

app.get('/health', (req, res) => {
	res.status(200).json({ status: 'OK' });
});

export default app
```

## `db/connection.ts`

```js
import mongoose from "mongoose";
const connectDB = async () => {
  try {
    const dbConnectionInstance = await mongoose.connect(
      `${process.env.MONGO_URI}/${process.env.DB_NAME}`
    );
    console.log(`Database Connected: ${dbConnectionInstance.connection.host}`);
  } catch (error) {
    console.log(
      "Some error occurred while connecting to database",
      error.message
    );
  }
};

export default connectDB;
```

## `index.ts`

```js
import dotenv from "dotenv"
dotenv.config()
import { connectDB } from "./db/connection"
import app from "./app"

connectDB()
	.then(() => {
		app.on("error", (error) => {
			console.log("ERR: ", error);
			throw error;
		});

		app.listen(process.env.PORT || 8000, () => {
			console.log(`Server is running at ${process.env.PORT}`);
		});

	})
	.catch((err) => {
		console.log("Mongo DB connection FAILED!!!!", err);
	});
```