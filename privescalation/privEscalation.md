# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
- There is no session, so the user id and the role are attacker defined, thus allowing an attacker to arbitrarly change the role of users.
2. Briefly explain how a malicious attacker can exploit them.
- An attacker can brute force user ids until one of them gives them authorized access to change the role of a user. This allows the attacker use 'admin' powers to change the role of some users. 
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
- We can use a session to authorize the user rather than some value from the body. Because the session is controlled by the server, we can trust that value. Assuming our session logic is robust, this prevents this vulnerability by not allowing the attacker to arbitrarily specify their identity.