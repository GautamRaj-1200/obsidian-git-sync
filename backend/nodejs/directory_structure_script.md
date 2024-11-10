## Run this script to create directory structure
```bash
mkdir server

mkdir server/src

mkdir server/src/controllers server/src/db server/src/middlewares
mkdir server/src/models server/src/routes server/src/types
mkdir server/src/utils

touch server/src/app.ts server/src/index.ts
touch server/src/controllers/.gitkeep
touch server/src/db/.gitkeep server/src/middlewares/.gitkeep
touch server/src/models/.gitkeep
touch server/src/routes/.gitkeep server/src/types/.gitkeep
touch server/.env server/.gitignore
```

### Run this script to create directory structure with starter code in `app.ts`, `index.ts` and `db/connection.ts`

```bash
#!/bin/zsh

mkdir server

mkdir server/src

mkdir server/src/controllers server/src/db server/src/middlewares
mkdir server/src/models server/src/routes server/src/types
mkdir server/src/utils

touch server/src/app.ts server/src/index.ts
touch server/src/controllers/.gitkeep
touch server/src/db/connection.ts server/src/middlewares/.gitkeep
touch server/src/models/.gitkeep
touch server/src/routes/.gitkeep server/src/types/.gitkeep
touch server/.env server/.gitignore

cat <<\EOF > server/src/app.ts
import express from "express";
import cors from "cors";
import cookieParser from "cookie-parser";
const app = express();

app.use(
    cors({
        origin: process.env.CORS_ORIGIN,
        credentials: true,
    })
);

app.use(express.json({ limit: "16kb" }));
app.use(express.urlencoded({ extended: true, limit: "16kb" }));
app.use(express.static("public"));
app.use(cookieParser());

app.get("/health", (req, res) => {
    res.status(200).json({ status: "OK" });
});

import authRouter from "./routes/auth.routes.js";
import postRouter from "./routes/post.routes.js"
import userRouter from "./routes/user.routes.js"

app.use("/api/v1/auth", authRouter);
app.use("/api/v1/posts", postRouter)
app.use("/api/v1/users", userRouter)

export default app;
EOF

cat <<\EOF > server/src/index.ts
import app from "./app.js";
import dotenv from "dotenv";
dotenv.config();
import { connectDB } from "./db/connection.js";

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
EOF

cat <<\EOF > server/src/db/connection.ts
import mongoose from "mongoose"

export const connectDB = async () => {
    try {
        const dbConnectionInstance = await mongoose.connect(`${process.env.MONGODB_URI}/${process.env.DB_NAME}`)
        console.log("MongoDB Connected!!!!! Connection Instance: ", dbConnectionInstance.connection.host)
    } catch (error) {
        let errorMessage = "Failed!!!"
        if (error instanceof Error) {
            errorMessage = error.message;
        }
        console.log("Error occurred while connecting to DB: ", errorMessage)
    }
}
EOF



```