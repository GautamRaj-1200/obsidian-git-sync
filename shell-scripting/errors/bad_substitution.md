## Error happened when running a script to setup node project
- The script: I was writing
```bash
cat <<EOF > server/src/app.ts
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
```
- It would result in ***"Bad Substitution"*** error
**REASON AND FIX**
- The error "Bad substitution" is occurring because of how EOF heredocs interact with special characters in TypeScript code. 
- The main changes I made to fix the "Bad substitution" errors:
	1. Added `\` before the `EOF` heredoc markers (like `<<\EOF`) for all three file creation blocks. This tells the shell to treat the content literally and not try to expand variables.
	2. The error was occurring because the shell was trying to interpret the `${...}` syntax in the TypeScript code as shell variables, but by using `<<\EOF` instead of `<<EOF`, we prevent this interpretation.