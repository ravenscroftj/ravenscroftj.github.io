

- ## Resolving Runtime Issues in [[Alpine]]-based Docker
	- You may see an error similar to `Unable to load Node-API Library from /src/node_modules/.prisma/client/libquery_engine-linux-musl.so.nod`
	- This is to do with the libraries available by default in alpine-based docker images
	- Add a `RUN` command to your docker build image before the `npx prisma generate` step:
	  
	  ```dockerfile
	  RUN apk add --update --no-cache openssl1.1-compat
	  ```
	-
	- Prisma Github issue covering this problem [here](https://github.com/prisma/prisma/issues/14043#issuecomment-1347948974)
	- #+BEGIN_IMPORTANT
	  If you have a multi-step build then you may need to add the openssl-compat module to both the builder and the runtime environment.
	  #+END_IMPORTANT
	  
- ## Timestamps
	- add `@default(now())` for `createdAt` fields
	- add `@updatedAt` for `updatedAt` fields
	-