# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?id[$ne]=
    ```

4. Do you see the server crashing?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.
- The potential vulnerability is that unsanitized input is being provided to query the _id field, which leads to the server crashing. Additionally, there is no rate limiter, so attackers can overwhelm the server.
2. Briefly explain how a malicious attacker can exploit them.
- A malicious attack can crash the server by crafting an input userinfo which is an invalid _id, which can then crash the application. Attackers could also send many requests within a second to overwhelm the server.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
- The secure version simply handles the error using a try/catch block. This prevents the server from crashing if an invalid id is passed. The server also uses a rate limiter middleware to prevent the server from being spammed.