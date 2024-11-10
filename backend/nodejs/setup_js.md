## Install
- `npm i -D prettier nodemon rimraf`
- `npm i bcrypt cookie-parser cors dotenv express jsonwebtoken mongoose nodemailer`
## `app.js`

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

## `db/connection.js`

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

## `index.js`

```js
import app from "./app.js";
import dotenv from "dotenv";
dotenv.config();
import connectDB from "./db/connection.js";

connectDB()
  .then(() => {
    const server = app.listen(process.env.PORT || 8000, () => {
      console.log(`Server is running at ${process.env.PORT}`);
    });
    server.on('error', (error) => {
      console.error("Server error: ", error);
      process.exit(1);
    });
  })

  .catch((err) => {
    console.log("Mongo DB connection FAILED!!!!", err);
  });
```