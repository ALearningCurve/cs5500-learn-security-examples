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
- One potential vulnerability is unsanitized input provide by users is directly being used to query the _id field, which leads to the server crashing if the _id is not valid. Additionally, there is no rate limiter, so attackers can overwhelm the server with many requests. Ultimately, both result in the server being unavailable to other users, thus these vulnerabilities are examples of denial of service attacks.
2. Briefly explain how a malicious attacker can exploit them.
- A malicious attacker can crash the server by crafting malicious input to userinfo containing an invalid _id (i.e. some string like 'hello'), which can then crash the application since it is not a valid mongo id. Attackers could also send many requests within a second to overwhelm the server and thus prevent it from responding in a timely manner to real requests.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
- The server no longer crashes on malicious input to the userinfo route by handling the error using a try/catch block. This prevents the server from crashing if an invalid id is passed, since any error with the _id would be caught. The server also uses a rate limiter middleware to prevent the server from being spammed. This helps to prevent the server from being overwhelmed by malicious requests. Both changes make the server more well defended against DoS attacks.